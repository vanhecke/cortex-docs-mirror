---
description: >-
  Using advanced settings while creating your outpost, you can deploy a Cortex
  Cloud Azure outpost using your own pre-created Entra ID app registration.
---

# Working with Bringing your own Azure app (BYOA) outposts

{% hint style="info" %}
**License type**: This feature is included with a Cortex XSIAM Premium license. It is also included with any other Cortex XSIAM product that has the Cloud Runtime Security add-on.
{% endhint %}

Use the Bring Your Own App (BYOA) custom outpost to deploy a Cortex XSIAM Azure outpost using your own pre-created Entra ID app registration. This type of outpost is designed for organizations with strict governance policies that require control over Entra ID tenant-level resources.

{% hint style="info" %}
**Important!** Once deployed, the outpost mode cannot be changed. If you deploy with BYOA, you cannot switch to a non-BYOA outpost deployment later (or vice versa). Choose your mode before deployment.
{% endhint %}

## How BYOA outposts differ from standard outposts

With a standard Azure outpost without BYOA, Cortex generates the app registration and its federated identity credentials in your tenant during Terraform apply, using tenant-scoped `Application.ReadWrite.All`.

With BYOA:

* You (not Cortex) own the app registration in your Entra ID directory.
* The Terraform runner holds only object-scoped ownership on that one app registration, not any tenant-wide permission.
* Cortex never writes to your tenant beyond that single app registration.

## Who provides what?

The following table presents what your provide vs. what Cortex creates for you.

| You create (once)                                          | Cortex creates during Terraform apply                         |
| ---------------------------------------------------------- | ------------------------------------------------------------- |
| The Entra ID app registration and its service principal    | All federated identity credentials on your app registration   |
| Optionally, the scanner managed identities (UAMIs)         | All outpost infrastructure (storage, networking, scanner VMs) |
| Ownership of the app registration for the Terraform runner | Scanner-managed identities (unless you provide your own)      |

## Work flow

The following work flow presents a high-level order of tasks to configure and work with Azure BYOA outposts:

1. Check and meet the prerequisites.
2. Create the app registration and service principal in your Entra ID tenant, either with a shell script Palo Alto Networks provides or in the Azure portal. Save the IDs for use in the next task.
3. Run the Create Outpost wizard to define the outpost using BYOA app registration IDs and download the Terraform. Deploy the outpost by executing the downloaded Terraform. You define the app registration IDs, and Cortex handles everything else, such as Federated Identity Credentials (FICs), managed identities, infrastructure, and role assignments.
4. Verify the outpost.
5. After outpost deployment, BYOA covers only the app-registration side of the outpost.

## What's next?

[Task 1: Meet the prerequisites for Azure BYOA outposts](working-with-bringing-your-own-azure-app-byoa-outposts/task-1-meet-the-prerequisites-for-azure-byoa-outposts)
