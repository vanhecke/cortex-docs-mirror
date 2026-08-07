# Prevent malicious LDAP queries

Active Directory (AD) routinely processes millions of legitimate queries from users and services. Threat actors frequently exploit this open architecture during the reconnaissance phase of an attack to map the network, identify privileged users, and discover attack paths without triggering standard security alarms. &#x20;

To accurately distinguish between legitimate administrative queries and malicious reconnaissance, ITDR analyzes the context of LDAP traffic in real time. Instead of viewing a single query in isolation, ITDR evaluates it in context to reveal malicious intent.

The module continuously evaluates traffic across four key behavioral dimensions:

1. Source of query: Analyzes whether the request originates from a known, trusted admin workstation or an anomalous, unverified endpoint.
2. Number of queries (volume): Monitors for massive spikes in read operations. Normal business logic usually involves looking up a few contacts, whereas reconnaissance tools query thousands of objects in seconds.
3. Contextual patterns: Flags activity if a user suddenly deviates from their standard historical behavior or performs lookups that do not align with their role.
4. Query attributes: Identifies specific search filters that are highly valuable to attackers but rarely used in typical operations (such as searches for `adminCount=1` or unconstrained delegation).

The module identifies and blocks the unique signatures of specific reconnaissance tools at the source. Rather than generating generic alerts, ITDR provides precise alerts, for example, "Attack detected via BloodHound".

### Key Benefits

Implementing this protection provides you with two primary advantages:

* Real-Time prevention: Stops attacks proactively during the reconnaissance phase. By blocking the LDAP queries, the system blinds the attacker and forces them to operate without a map of your environment.
* Enriched analytics: Every blocked query is fed back into the Cortex ITDR analytics engine. This data generates detailed issues within Cortex XSIAM, giving you actionable intelligence on exactly which tool was being used and who the attacker was targeting.

To enable LDAP protection, toggle the **LDAP protection** setting in the Identity profile of the agent. To  configure the Identity profile, see [Set up Identity Profiles](broken-reference).
