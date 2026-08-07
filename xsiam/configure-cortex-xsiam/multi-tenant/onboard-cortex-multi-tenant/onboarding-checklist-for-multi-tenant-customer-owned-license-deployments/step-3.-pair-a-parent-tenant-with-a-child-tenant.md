# Step 3. Pair a parent tenant with a child tenant

After you set up the correct access configurations and role permissions, you should pair the parent tenant to the child tenants.

Cortex enables parent-child pairing between tenants located in different geographical regions. To enable this capability, contact your support team.

**Pairing a Parent and Child Tenant**

1.  Log in to the Cortex XSIAM tenant that has been assigned as the parent tenant and select Settings → Configurations → Tenant Management.

    The Tenant Management table displays:

    * Tenant Name: Name of the child tenant.
    * Pairing Status: State of a pairing request: Paired, Pending, Failed, Rejected.
    * Account Name: CSP account to which the child tenant is associated.
    * Last Sync: Timestamp of when the parent tenant last made contact with child tenant.
    * Managed Security Actions: A column for each security action with a status: Configuration name or Unmanaged. Unmanaged status means that a configuration for the security action has not yet been selected.
    * Region: Shows the region of the child tenant.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>This field is not enabled by default. To enable this, contact your support team.</p></div>
2.  Click + Pair Tenant.

    You can pair tenants across different regions.
3.  In the Pair Tenant window, select the child tenant you want to pair.

    Child tenants are grouped according to:

    * Unpaired: Children that have not yet been paired and are available. If another parent has requested to pair with the child but the child has not yet agreed, the tenant will appear.
    * Paired: Children that have already been paired to this parent.
    * Paired with others: Children that have been paired with other parents.
    * Pending: Children with a pending pairing request.
4.  Pair the tenant.

    Cortex XSIAM then sends a Request for Pairing to the specified child tenant.
5. In the child tenant Cortex XSIAM console, a child tenant user with Admin role permissions needs to approve the pairing by navigating to Notifications [![notification-icon.png](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABoAAAAaCAYAAACpSkzOAAAACXBIWXMAABYlAAAWJQFJUiTwAAAAB3RJTUUH4wwCBhsvNZdsdwAAAAd0RVh0QXV0aG9yAKmuzEgAAAAMdEVYdERlc2NyaXB0aW9uABMJISMAAAAKdEVYdENvcHlyaWdodACsD8w6AAAADnRFWHRDcmVhdGlvbiB0aW1lADX3DwkAAAAJdEVYdFNvZnR3YXJlAF1w/zoAAAALdEVYdERpc2NsYWltZXIAt8C0jwAAAAh0RVh0V2FybmluZwDAG+aHAAAAB3RFWHRTb3VyY2UA9f+D6wAAAAh0RVh0Q29tbWVudAD2zJa/AAAABnRFWHRUaXRsZQCo7tInAAAEA0lEQVRIiaWWbWxTZRTHf0/X3rUdrGs3y1a6F9Yx5jZezDDOqEFBxUQlmH0gRmLUTAODDJPxBTRgfP0g8QMfjCSaKEbNFviixBAxxkAImqgszL2Y2rHupY7MrXuBbrtr+/jhdu29a9ex2Nz0n3N6nqfnf/7Pfc4R+b46iQQE3D1KEEKzQftBCM2/zEJzyhRIZNb97fY8CvLXMK+qjIfDml+AlCIRJ5L/l8TEepNM5iQXc8uAkvy1azny6ktc6jjLmQ/fpbamWlslyYCkMLGPSctFY5R4UjYkv6sqytjftIe2k+8zO6fyYtNebFYbQiSiDUiabUoxkSQeA0Oz2UJtdRXPP7cHgOs9vQyFQvjKy3hg+zbcRYWGehgZpewcq8v9lpaB0GWiodORz2v793GyrZU19jw6vrvIz1evEY/HqSwr5ZV9TWzbXIf/ZpCxf8eXMNJVChDLnTpngYPjrS3sfPhBPjj9MZeuXGVqaibJV1Fy8ZV7Od56CJfLyRvvnaKzpzt9owRm1MhkMrF7xyPsfKiRQ8dOcO7CRaanZwy1X1hQ6fX3c+TE20yEJ2lraabY7V6dRqWeElpefoHP28/zyx+dhtOjiwZgIjzFOx+dpsLrYUfj/ctqZMp0yuo3VWO32em48L3uFOpRpGwBgYFBfu/qpnH7fbgKHEatSTJazDT1Hm2tu5fAQBB1Xk1jkMx00S8hFo9x/UY3DVs2k2fP08VleY/MOWaKCp0EBgaZnJ7JyEDPf9H+rauLIpeTeDxmjFtOo9xchQqvh9GxMaSUS7RJ12iR4Xh4CoDS9R4j8+U0sioKNpud0K1bhhpn0wgEC6pKcDiE17NO58+ikUVRKPd6GP5nNCsD400gmZtXiUQieNzrdHFZNCp0aadmaHg0K4OlGqmqSnAkRLG7CJNIv/vSNKrxVRIcDjGnzhsyWkmjhViUyOwsXo8HRcnNrlFNVSXPPvE44alpotGoocYraSSAP3v9VHg9PPPkY1gsZsO6pEZWq5W2A8141xfz2VftTM3MZGWwVCMp4YfLl/m18wbHDh+g+B63oRLmxc5qzsnB5XTw9flv6Qv04y0uWbHjZsIv2s/x9K5Hadhaz1AolOy0Zr1GsVicowebOXqwmf/7GRwJJZgmiu3w1UmtxwuqfRuYnZ0z9nwBFrOFjRs3MDg0wu3bdzCZcigvLeHN1w/T/ZefM2e/4U4kolsnUSwWAsFgaha5mynI6cjnx44vGRgcpu/vADabjYYt9fT5A5z65FP8/TdXLKpw+OqllBIhdFNQgqHm1+zaTVXsfWo3edZcEILOnh5+unKNicnJtAok99Pbq53rFEUhHosSjcdXNddl7EfZcGFBJRqLr3BTpN91/wGCjBMPnCzlqAAAAABJRU5ErkJggg==)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/zpngudZ5drlbO1Xgo0OgkA-5CAbsl8idaK8R43ZLhoTOw), locate the Request for Pairing notification and select Approve.
6.  Verify the parent-child pairing.

    After pairing has been approved, in the child tenant’s Cortex XSIAM app, when navigating to a page managed by a parent configuration, the child user is notified by a flag who is managing their security.

    In the child tenant’s, pages that you manage, appear with a read-only banner. Child tenant users cannot perform any actions from these pages, but can view the configurations you create on their behalf.

    | [![child-managed-read-only-banner.png](https://docs-cortex.paloaltonetworks.com/api/khub/maps/5CAbsl8idaK8R43ZLhoTOw/resources/SggXfrQeoEcBKJAMvSLdtQ-5CAbsl8idaK8R43ZLhoTOw/content?v=1320083d35522c75\&Ft-Calling-App=ft/turnkey-portal)](https://docs-cortex.paloaltonetworks.com/viewer/attachment/5CAbsl8idaK8R43ZLhoTOw/SggXfrQeoEcBKJAMvSLdtQ-5CAbsl8idaK8R43ZLhoTOw) |
    | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
