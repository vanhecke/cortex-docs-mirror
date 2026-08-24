---
description: Schedule XDR Collector upgrades for Cortex XSIAM.
---

# Configure XDR Collector upgrade scheduler

You can configure the Cortex XDR Collector upgrade scheduler and the number of parallel upgrades.

You can configure the Cortex XDR Collector upgrade scheduler and the number of parallel upgrades. There can be a maximum of 500 parallel upgrades scheduled in a week, which is the default configuration at any time of day.

To define the XDR Collector upgrade scheduler and number of parallel upgrades.

1. In Cortex XSIAM, select Settings → Configurations → XDR Collectors → Configuration.
2. Set the XDR Collectors Configurations settings.

* `Amount of Parallel Upgrades`: Specify the number of parallel upgrades, where the maximum number is 500 (default).
* `Days in Week`: Select the specific days in the week that you want the upgrade to occur, where the default is configured as every day in the week.
* `Schedule`: Select whether you want the upgrade to be at Any time (default) or at a Specific time. When setting a specific time, you can set the From and To times.

3. Click Save.
