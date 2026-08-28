# Activate DSPM Database

{% hint style="info" %}
**License**

This feature is included with a Cortex XSIAM Premium license. It is also included with a Cortex XSIAM NG SIEM and Cortex XSIAM Enterprise license that has the Cloud Posture Security or Cloud Runtime Security add-on.
{% endhint %}

The DSPM Database applet is an application installed directly onto the Broker VM. It is the core component responsible for auditing and securing your on-premises PostgreSQL and MySQL databases, providing visibility into the risks associated with your stored data.

Once configured, this applet continuously:

* Accesses your on-premise databases, including those containing regulated or confidential information.
* Identifies data that must be stored in accordance with specific compliance standards.
* Classifies database content to identify sensitive information.
* Transmits the collected insights and risk metadata securely through the Broker VM to Cortex XSIAM.

The DSPM Database applet provides insights into risks associated with data stored in on-premise databases, PostgreSQL and MySQL instances. Whether you are transitioning to the cloud or maintaining assets on-premise, activating this applet offers a customizable way to manage data security and compliance within a single, unified platform.

{% hint style="warning" %}
**Prerequisite**

* [Set up and configure Broker VM](broken-reference).
* Know the database engine, host, and port for the database you want to connect.
{% endhint %}

### How to activate the DSPM Database applet

1. Select **Settings** → **Configurations** → **Data Broker** → **Broker VMs**.
2.  Do one of the following:

    * On the **Brokers** tab, find the Broker VM, and in the **APPS** column, left-click **Add** → **DSPM Database**.
    * On the **Clusters** tab, find the Broker VM, and in the **APPS** column, left-click **Add** → **DSPM Database**.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>The applet list displays only the applets for which you have permissions.</p></div>
3.  Configure the **DSPM Database** settings.\
    **Database Connection**

    | Field           | Description                                                                                                                                                                      |
    | --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | Database Engine | Select **PostgreSQL** or **MySQL** in the list.                                                                                                                                  |
    | Host            | Enter host name.                                                                                                                                                                 |
    | Port            | Enter port.                                                                                                                                                                      |
    | Database Name   | Enter the name of the database.                                                                                                                                                  |
    | Enable SSL      | Decide whether to turn on the **Enable SSL** toggle, which ensures that the connection between the applet and your on-premise database is encrypted, protecting data in transit. |
    | Username        | Enter your user name.                                                                                                                                                            |
    | Password        | Enter your password.                                                                                                                                                             |
    | Test Connection | Select to validate the connection permissions.                                                                                                                                   |

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p><strong>Note</strong></p><p>By default, all configured connections are saved.</p></div>
4. (Optional) Click **Add Connection** to define another database connection. You can add multiple connections under one DSPM Database applet instance.
5. Activate the DSPM Database applet.\
   After a successful activation, the **APPS** field displays DSPM Database with a green dot indicating a successful connection.

### Other actions

Once the DSPM Database applet is activated, you can perform the following actions:

* **Edit**
* **Deactivate**: On the **Broker VMs** screen, in the **ADD** column, in the context menu, click **Deactivate**.
* **Delete**: On the **Database Connection** screen, click the **Delete** icon next to the connection you want to remove.
* **Scan**: Turn on the **Classification** toggle. This enables 2.500 random files to be scanned classified each time.
* **Select Cadence**: In the **Scan every** list, select the cadence of how often the files are to be scanned. If you want the scans to occur less frequently, choose the Custom option and enter the amount of days, weeks, or months that you require.

### Inventory list

Each new connection that is created correlates to an asset in the inventory. You can see the connections by clicking **Inventory** → **All Assets** → **Data** → **Databases**. Make sure to set the filter to `Provider = On Premise`.
