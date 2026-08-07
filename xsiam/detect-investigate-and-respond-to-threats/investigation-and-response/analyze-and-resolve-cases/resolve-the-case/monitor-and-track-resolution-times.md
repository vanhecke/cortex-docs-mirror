# Monitor and track resolution times

By default, the system tracks the resolution of cases and issues using built-in fields: **Resolution Timer** and **Resolution SLA**. You can use these fields to monitor deadlines at a glance or sort by SLA status. These fields are available for tracking case resolution on the **Cases** page, and issue resolution on the **Issues** page.

### Resolution Timer

Automatically tracks the total duration from creation to resolution. The timer stops when the status changes to Resolved.

{% hint style="info" %}
#### Timer behavior after reopening

If a case or issue is reopened, the timer resumes and includes the entire elapsed time, including the period when it was closed.
{% endhint %}

### Resolution SLA

Measures your compliance against defined SLA targets. By default, no SLA rules are preconfigured, giving you the flexibility to define SLAs that work best for your environment.

Once configured, the system evaluates the rules in order and the first matching rule is applied. You can configure SLAs for your cases and issues, as explained in [Create an SLA rule](../../../../configure-cortex-xsiam/customize-cases-and-issues/create-slas-for-issue-resolution).

#### Case SLAs

To ensure high-level visibility and help you adhere to your organizational goals, all active SLAs are visible directly within the product workflows:

* **Real-time visibility:** When you open a case, the status of all active SLAs are displayed directly in the case header.
* **Parallel SLA tracking:** Cases support running multiple SLAs concurrently. While the default **Resolution SLA** tracks the baseline lifecycle, you can create additional SLA fields to measure separate milestones, such as initial response times, or to enforce unique targets for specific customer tiers. For more information about setting up additional case SLAs, see [Create case timers and SLAs](../../../../configure-cortex-xsiam/customize-cases-and-issues/create-slas-for-issue-resolution/create-case-timers-and-slas).
* **Table filtering and sorting:** The predefined **Resolution SLA** field and any additional SLA fields can be monitored in the **Cases** table, allowing you to filter, sort, and prioritize your queue by custom compliance metrics. For more information, see [Monitor the status of issue resolution SLAs](../../../../configure-cortex-xsiam/customize-cases-and-issues/create-slas-for-issue-resolution).
