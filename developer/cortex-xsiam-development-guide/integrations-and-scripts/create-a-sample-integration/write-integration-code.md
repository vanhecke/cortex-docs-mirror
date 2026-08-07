---
description: Write integration code for a sample integration.
---

# Write integration code

Once we've finished adding our parameters, command, argument, and outputs, we can write the integration code.

{% hint style="info" %}
### Note

The sample code uses standard Python error handling mechanisms, such as `try`. For more information about errors and exceptions in Python, see the [Python documentation](https://docs.python.org/3/tutorial/errors.html). In our integration code, we raise exceptions when errors occur. The convention is to have a main try/except block on `main()` that catches errors and calls `return_error`.

The `return_error` function ensures that playbooks calling these functions will fail and stop, alerting the user to a problem. In integrations and scripts, we refrain from calling `return_error` in other places in the code.
{% endhint %}

**Import**

To begin, we have the option to import Python libraries, so that their commands are available for our integration. Every integration runs inside a Docker image, and our standard Docker image includes most of the common packages, such as JSON and collections. In our Yoda Speak integration, we don’t need to import any libraries, as it only uses the `BaseClient` class, implicitly imported from CommonServerPython.

When working in Visual Studio Code, we recommend importing the following at the top of your code for [debugging](../../testing/debugging) purposes.

```programlisting
# uncomment the import statements for debugging in PyCharm, VS Code or other IDEs.
# import demistomock as demisto
# from CommonServerPython import *  # noqa # pylint: disable=unused-wildcard-import
# from CommonServerUserPython import *  # noqa
```

If you want to use Python libraries that are not included in the standard Cortex XSIAM Docker image, you can create a customized Docker image.

**Define the prefix for the output context keys**

Set the term Phrase as a prefix for the output context keys.

```programlisting
TRANSLATE_OUTPUT_PREFIX = 'Phrase'
```

**Disable secure warnings**

Next we prevent Python from raising a warning when accessing resources insecurely.

```programlisting
# Disable insecure warnings
requests.packages.urllib3.disable_warnings()  # pylint: disable=no-member
```

Since we created the insecure parameter that allows the integration to ignore TLS/SSL certificate validation errors, we also need to disable the warning.

**Create the class client**

```programlisting
class Client(BaseClient):
    def __init__(self, api_key: str, base_url: str, proxy: bool, verify: bool):
       super().__init__(base_url=base_url, proxy=proxy, verify=verify)
       
       self.api_key = api_key
       
       if self.api_key:
            self._headers = {'X-Funtranslations-Api-Secret': self.api_key}
 
    def translate(self, text: str):
        return self._http_request(method='POST', url_suffix='yoda', data={'text': text}, resp_type='json',  ok_codes=(200,))
```

The Client is an object that communicates with the API. We create a class called Client. When a Client object is created, it instantiates a parent BaseClient using the parameters we have set up (whether to use proxy, whether to allow insecure connections, and the base URL). If the user provided values to the `api_key` parameter, the Client sets the relevant headers it will use.

In this example, when using the [Yoda Speak API](https://funtranslations.com/api/yoda) with an API key, the API key is passed as a header.

The number of methods our Client class has usually matches the number of commands in our integration. The Yoda Speak integration only has the translation command, so our Client object should have a matching method to the API request which returns its result.

**Create the test\_module**

```programlisting
def test_module(client: Client) -> str:
    """
    Tests API connectivity and authentication'

    Returning 'ok' indicates that connection to the service is successful.
    Raises exceptions if something goes wrong.
    """

    try:
        response = client.translate('I have the high ground!')

        success = demisto.get(response, 'success.total')  # Safe access to response['success']['total']
        if success != 1:
            return f'Unexpected result from the service: success={success} (expected success=1)'

        return 'ok'

    except Exception as e:
        exception_text = str(e).lower()
        if 'forbidden' in exception_text or 'authorization' in exception_text:
            return 'Authorization Error: make sure API Key is correctly set'
        else:
            raise e
```

The `test_module` function is run whenever the **Test** integration button is clicked in the integration instance settings. The `test_module` function sends a hard coded preset string (here, it’s `I have the high ground`) to the Yoda-Speak translate API to test API connectivity and authentication. There are three possible results:

* HTTP response code is 200, which means the request is successful. We return the string `ok` per the convention for a successful test.
* The request is not successful and the problem is related to authorization: `Authorization Error: make sure API Key is correctly set`.
* The request is not successful for any other reason: The error text is displayed.

**Create the translate\_command**

```programlisting
def translate_command(client: Client, text: str) -> CommandResults:
    if not text:
        raise DemistoException('the text argument cannot be empty.')

    response = client.translate(text)
    translated = demisto.get(response, 'contents.translated')

    if translated is None:
        raise DemistoException('Translation failed: the response from server did not include `translated`.',
                               res=response)

    output = {'Original': text, 'Translation': translated}

    return CommandResults(outputs_prefix='YodaSpeak',
                          outputs_key_field=f'{TRANSLATE_OUTPUT_PREFIX}.Original',
                          outputs={TRANSLATE_OUTPUT_PREFIX: output},
                          raw_response=response,
                          readable_output=tableToMarkdown(name='Yoda Says...', t=output))
```

The `translate_command` function uses the client that is provided as an argument for the function and it calls translate using the text provided. The client is created outside of the function (in `main()`). The function performs several steps.

1. Confirms that there is a non-empty string to translate. If the string input is empty, it raises an exception.
2. Tells the Client to send the appropriate API call. If the translation fails (for example due to an API rate limit, authentication, or connection error), an exception is raised.
3. If the translation succeeds, we want to return it to Cortex XSIAM. To do that, we use a class called `CommandResult` (which is declared in CSP). We supply it with the following arguments:
   * `outputs`: We create a dictionary called `outputs` where both the original text and the translation are stored.
   * `outputs_prefix`: The first level of the output in the context data. It usually matches the name of the integration or service.
   * `raw_response`: The argument used to attach the raw response received from the service, which can be useful when debugging unexpected behaviors.
   * `outputs_key_field`: Since we can run the translation command multiple times, and possibly receive different results for the same string of text, the system needs to know where to update or append each result. In this example we tell the system that `Phrase.Original` is the key that represents the original text we translated, so that the next time the command is run on the same string of text, the translated values will update.
   *   `readable_output`: This is what users see in the War Room when calling the command, so it should be formatted. We can use the `tableToMarkdown` function (from CSP) to turn the JSON into a user-friendly table. We provide `tableToMarkdown` with both the JSON values and a title for the table.

       <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Tip</h3><p>The Script Helper provides an easy way to insert common functions into your code. If you click the Script Helper button and search for the <code>tableToMarkdown</code> command, you have the option to insert it directly into the code with placeholders for its <code>name</code> (title) and <code>t</code> (JSON) arguments.</p></div>

**Create the Main function**

Everything actually runs within `main`. We pull in the integration parameters, arguments, and the translate command. The parameters are assigned to variables. Notice that the parameters are the same ones we set up in the integration settings earlier.

```programlisting
def main() -> None:
    params = demisto.params()
    args = demisto.args()
    command = demisto.command()

    api_key = params.get('apikey', {}).get('password')
    base_url = params.get('url', '')
    verify = not params.get('insecure', False)
    proxy = params.get('proxy', False)
```

When the function runs, the command will be logged for debugging purposes.

```programlisting
demisto.debug(f'Command being called is {command}')
```

We now create a Client using the given parameters. The Client is defined.

```programlisting
try:
    client = Client(api_key=api_key, base_url=base_url, verify=verify, proxy=proxy)
```

There are two possible commands that can be passed to the main function in our integration.

1.  `test-module`: If the command name is `test-module`, it means the user has clicked the integration **Test** button while setting up or editing an integration instance.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>We did not explicitly create a command called <code>test-module</code>. It is a built-in command.</p></div>

    When returning `ok`, the user is shown a green `Success` message. If any value other than `ok` is returned, an error is displayed. Make sure you return errors that help the user understand what to change in the integration settings in order to fix connection issues.
2. `yoda-speak-translate`: This is the primary command for our integration and lets us translate strings of text.

```programlisting
if command == 'test-module':
    # This is the call made when clicking the integration Test button.
    return_results(test_module(client))

elif command == 'yoda-speak-translate':
    return_results(translate_command(client, **args))

else:
    raise NotImplementedError(f"command {command} is not implemented.")
```

There is also an `else` option. This returns an error if someone tries to run a command that was created in the YAML file but does not exist in the Python (PY) file. For example, if you added a command `yoda-interpret` in the integration settings, but did not add it to this file, and then tried to run that command, you would see `Yoda-interpret is not implemented`.

**Log errors**

```programlisting
# Log exceptions and return errors
except Exception as e:
    demisto.error(traceback.format_exc())  # print the traceback
    return_error("\n".join(("Failed to execute {command} command.",
                            "Error:",
                            str(e))))
```

If any errors occur during the execution of our code, show those errors to the user and also return an error.

**Start at Main**

```programlisting
if __name__ in ('__main__', '__builtin__', 'builtins'):
    main()
```

This line tells the system where to start running our code. By convention, we call the main function `main`.
