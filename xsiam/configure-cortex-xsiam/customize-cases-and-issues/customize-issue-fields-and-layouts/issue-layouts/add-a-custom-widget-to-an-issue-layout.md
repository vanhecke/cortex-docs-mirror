---
description: >-
  Add custom or system widgets to Cortex XSIAM issue layouts with
  dynamic-section scripts and layout rules.
---

# Add a custom widget to an issue layout

You can add a custom or system widget to a custom issue layout by uploading an auto script and using it in a **General Purpose Dynamic Section** in your layout.

The following example shows how to add an Indicator Widget Bar. This custom widget script shows the severity of indicators in an issue, as a bar chart.

1.  Add the Indicator Widget Bar script to Cortex XSIAM.

    1. Go to **Investigation & Response** → **Automation** → **Scripts** and upload the following script:

    ```
    commonfields:
      id: ee3b9604-324b-4ab5-8164-15ddf6e428ab
      version: 49
    name: IndicatorWidgetBar
    script: |-
      # Constants
      HIGH = 3
      SUSPICIOUS = 2
      LOW = 1
      NONE = 0

      indicators = []
      scores = {HIGH: 0, SUSPICIOUS: 0, LOW: 0, NONE: 0}
      incident_id = demisto.incidents()[0].get('id')

      foundIndicators = demisto.executeCommand("findIndicators", {"query":'investigationIDs:{}'.format(incident_id), 'size':999999})[0]['Contents']

      for indicator in foundIndicators:
          scores[indicator['score']] += 1

      data = {
        "Type": 17,
        "ContentsFormat": "bar",
        "Contents": {
          "stats": [
            {
              "data": [
                scores[HIGH]
              ],
              "groups": None,
              "name": "high",
              "label": "incident.severity.high",
              "color": "rgb(255, 23, 68)"
            },
            {
              "data": [
                scores[SUSPICIOUS]
              ],
              "groups": None,
              "name": "medium",
              "label": "incident.severity.medium",
              "color": "rgb(255, 144, 0)"
            },
            {
              "data": [
                scores[LOW]
              ],
              "groups": None,
              "name": "low",
              "label": "incident.severity.low",
              "color": "rgb(0, 205, 51)"
            },
            {
              "data": [
                scores[NONE]
              ],
              "groups": None,
              "name": "unknown",
              "label": "incident.severity.unknown",
              "color": "rgb(197, 197, 197)"
            }
          ],
          "params": {
              "layout": "horizontal"
          }
        }
      }

      demisto.results(data)
    type: python
    tags:
    - dynamic-section
    enabled: true
    scripttarget: 0
    subtype: python3
    runonce: false
    dockerimage: demisto/python3:3.7.3.286
    runas: DBotWeakRole
    				
    ```

    1. Click Save
2. Go to Settings → Configurations → Object Setup → Issues → Layout Rules → **New Rule**.
3. Enter a rule name, select the layout to use if the rule is met, and provide a description.
4. Search for issues that match the criteria you want to use for the layout rule. For example, you can search for issues from a specific issue source.
5. Click **Create**.
6. Repeat as needed to create multiple rules.
7. Click **Save**.
