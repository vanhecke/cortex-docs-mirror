# What's a BIOC?

Behavioral indicators of compromise (BIOCs) enable you to alert and respond to behaviors—tactics, techniques, and procedures. Instead of hashes and other traditional indicators of compromise, BIOC rules detect behavior related to processes, registry, files, and network activity.

To benefit from the latest threat research, the Cortex XSIAM tenant automatically receives pre-configured rules from Palo Alto Networks. These global rules are delivered to all tenants with content updates. When you need to override a global BIOC rule, you can disable it or set a rule exception. As you investigate threats on your network and endpoints, you can also configure additional BIOC rules. BIOC rules are highly customizable; you can create a BIOC rule that is simple or quite complex.

As soon as you create or enable a BIOC rule, the tenant begins to monitor input feeds for matches. It also analyzes historical data collected in the tenant. When there is a match on a BIOC rule, Cortex XSIAM generates an issue.

To further enhance the BIOC rule capabilities, you can also configure BIOC rules as custom prevention rules and incorporate them with your Restrictions profiles. The tenant can then generate behavioral threat prevention issues based on your custom prevention rules in addition to the BIOC detection issues.
