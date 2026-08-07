# Create a security managed action

After you have created and assigned a configuration for each of your child tenant’s security actions, you can define the specific managed action on behalf of the child tenant.

1. Navigate to each of the following Cortex XSIAM pages:
   * Investigation → Incident Management → Exclusions → **Alert Exclusions Configuration** panel
   * Investigation → Incident Management → Starred Alerts → **Starred Alerts Configuration** panel
   * Endpoints → Policy Management → Prevention → Profiles → **Profile Configuration** panel
   * Response → Action Center → Currently Applied Actions → Block List/Allow List → **Allow List/Block List** configuration panel
2.  In the corresponding **Configuration** panel, select the [action configuration](create-and-allocate-configurations) you created and allocated to your child tenant.

    The corresponding security action **Table** displays the actions managing the child tenant.
3.  Depending on the security action, select:

    * **+ Add Exclusion** to create an Alert Exclusion.
    * **+ Add Starring Configuration** to create a starred alert inclusion.
    * **+ New Profile** to create a new endpoint profile.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><h3>Note</h3><p>Profiles you create are automatically cloned to your child tenants.</p></div>
