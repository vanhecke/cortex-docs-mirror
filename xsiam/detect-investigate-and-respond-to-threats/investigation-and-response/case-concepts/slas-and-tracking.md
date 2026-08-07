# SLAs and tracking

{% hint style="info" %}
### Notice

This feature requires a Cortex XSIAM Premium, Cortex XSIAM Enterprise, or Cortex XSIAM NG SIEM license.
{% endhint %}

In Cortex XSIAM, Service Level Agreements (SLAs) are tracked using a combination of Timer fields and SLA fields. This system allows you to quantify performance and ensure that critical security cases are addressed within defined timeframes.

### **SLA configuration components**

* **Timers:** These fields count forward to measure the actual duration of an action. For example, a **Time to Assignment** timer starts when a case is created and stops when an owner is assigned.
* **SLA fields:** These fields count backward from a predefined goal. They visualize the time remaining until a deadline is breached, changing color, for example to red, if the goal is exceeded.
* **Severity-based goals:** You can define different SLA targets based on case severity. This ensures that Critical cases receive a faster response than Medium or Low severity cases.

For more information about configuring SLAs and timer fields, see [Create additional case timers and SLAs](../../../configure-cortex-xsiam/customize-cases-and-issues/create-slas-for-issue-resolution/create-case-timers-and-slas).
