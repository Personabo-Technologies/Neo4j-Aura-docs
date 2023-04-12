<div>

<div>

# Neo4j AuraDB overview

</div>

<div>

<div>

<div>

Neo4j AuraDB is a fully managed cloud graph database service.

</div>

<div>

Built to leverage relationships in data, AuraDB enables lightning-fast
queries for real-time analytics and insights. AuraDB is reliable,
secure, and fully automated, enabling you to focus on building graph
applications without worrying about database administration.

</div>

</div>

</div>

<div>

## Plans

<div>

<div>

AuraDB offers the following subscription plans: **AuraDB Free**,
**AuraDB Professional**, and **AuraDB Enterprise**.

</div>

<div>

Each plan offers different levels of functionality and support:

</div>

<div>

<table>
<caption>Table 1. Platform</caption>
<colgroup>
<col/>
<col/>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th></th>
<th><span>AuraDB Free</span></th>
<th><span>AuraDB Professional</span></th>
<th><span>AuraDB Enterprise</span></th>
</tr>
</thead>
<tbody>
<tr>
<td><p>Instance size</p></td>
<td><p>Limits on node and relationship counts</p></td>
<td><p>1GB - 64GB (RAM)</p></td>
<td><p>4GB - 384GB (RAM)</p></td>
</tr>
<tr>
<td><p>Automated upgrades and patches</p></td>
<td><p><span><i></i></span></p></td>
<td><p><span><i></i></span></p></td>
<td><p><span><i></i></span></p></td>
</tr>
<tr>
<td><p>Self-healing</p></td>
<td><p><span><i></i></span></p></td>
<td><p><span><i></i></span></p></td>
<td><p><span><i></i></span></p></td>
</tr>
<tr>
<td><p>Fault tolerant</p></td>
<td><p><span><i></i></span></p></td>
<td><p><span><i></i></span></p></td>
<td><p><span><i></i></span></p></td>
</tr>
<tr>
<td><p>Cloud tenancy</p></td>
<td><p>Multi-tenant</p></td>
<td><p>Multi-tenant</p></td>
<td><p>Single-tenant with VPC isolation, dedicated cloud infrastructure</p></td>
</tr>
<tr>
<td><p>Cloud providers</p></td>
<td><p>GCP</p></td>
<td><p>GCP</p></td>
<td><p>AWS, Azure, GCP</p></td>
</tr>
<tr>
<td><p>On-demand query logs</p></td>
<td></td>
<td><p><span><i></i></span></p></td>
<td><p><span><i></i></span></p></td>
</tr>
<tr>
<td><p>Service availability SLA</p></td>
<td></td>
<td></td>
<td><p>99.95% uptime</p></td>
</tr>
<tr>
<td><p>Console user management</p></td>
<td></td>
<td></td>
<td><p><span><i></i></span></p></td>
</tr>
<tr>
<td><p>Multi-availability zone clusters</p></td>
<td></td>
<td></td>
<td><p><span><i></i></span></p></td>
</tr>
<tr>
<td><p>Clone database</p></td>
<td></td>
<td><p><span><i></i></span></p></td>
<td><p><span><i></i></span></p></td>
</tr>
<tr>
<td><p>Pause database</p></td>
<td><p>Automatic after 3 days of inactivity</p></td>
<td><p>On demand</p></td>
<td><p>On demand</p></td>
</tr>
<tr>
<td><p>Resume database</p></td>
<td><p>On demand or auto-deleted after 90 days</p></td>
<td><p>On demand or auto-resumed after 30 days</p></td>
<td><p>On demand or auto-resumed after 30 days</p></td>
</tr>
</tbody>
</table>

</div>

<div>

<table>
<caption>Table 2. Tools integrations and ecosystem</caption>
<colgroup>
<col/>
<col/>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th></th>
<th><span>AuraDB Free</span></th>
<th><span>AuraDB Professional</span></th>
<th><span>AuraDB Enterprise</span></th>
</tr>
</thead>
<tbody>
<tr>
<td><p>Neo4j Browser</p></td>
<td><p><span><i></i></span></p></td>
<td><p><span><i></i></span></p></td>
<td><p><span><i></i></span></p></td>
</tr>
<tr>
<td><p>Neo4j Bloom data visualization</p></td>
<td><p><span><i></i></span></p></td>
<td><p><span><i></i></span></p></td>
<td><p><span><i></i></span></p></td>
</tr>
<tr>
<td><p>Standard procedure library (<a>APOC-core</a>)</p></td>
<td><p><span><i></i></span></p></td>
<td><p><span><i></i></span></p></td>
<td><p><span><i></i></span></p></td>
</tr>
<tr>
<td><p>Data Connector: Apache Spark</p></td>
<td><p><span><i></i></span></p></td>
<td><p><span><i></i></span></p></td>
<td><p><span><i></i></span></p></td>
</tr>
<tr>
<td><p>Data Connector: Apache Kafka</p></td>
<td><p><span><i></i></span></p></td>
<td><p><span><i></i></span></p></td>
<td><p><span><i></i></span></p></td>
</tr>
<tr>
<td><p>Data Connector: Business Intelligence (BI)</p></td>
<td><p><span><i></i></span></p></td>
<td><p><span><i></i></span></p></td>
<td><p><span><i></i></span></p></td>
</tr>
</tbody>
</table>

</div>

<div>

<table>
<caption>Table 3. Backup</caption>
<colgroup>
<col/>
<col/>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th></th>
<th><span>AuraDB Free</span></th>
<th><span>AuraDB Professional</span></th>
<th><span>AuraDB Enterprise</span></th>
</tr>
</thead>
<tbody>
<tr>
<td><p>Backup frequency/RPO</p></td>
<td></td>
<td><p>Daily</p></td>
<td><p>Hourly</p></td>
</tr>
<tr>
<td><p>Backup retention</p></td>
<td></td>
<td><p>7 day</p></td>
<td><p>90 day</p></td>
</tr>
<tr>
<td><p>On-demand point-in-time snapshots</p></td>
<td></td>
<td><p><span><i></i></span></p></td>
<td><p><span><i></i></span></p></td>
</tr>
</tbody>
</table>

</div>

<div>

<table>
<caption>Table 4. Security</caption>
<colgroup>
<col/>
<col/>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th></th>
<th><span>AuraDB Free</span></th>
<th><span>AuraDB Professional</span></th>
<th><span>AuraDB Enterprise</span></th>
</tr>
</thead>
<tbody>
<tr>
<td><p>Encryption (at rest, in transit)</p></td>
<td><p><span><i></i></span></p></td>
<td><p><span><i></i></span></p></td>
<td><p><span><i></i></span></p></td>
</tr>
<tr>
<td><p>DBMS level role-based access control</p></td>
<td></td>
<td></td>
<td><p><span><i></i></span></p></td>
</tr>
<tr>
<td><p>Fine-grained database security</p></td>
<td></td>
<td></td>
<td><p><span><i></i></span></p></td>
</tr>
<tr>
<td><p>Private VPC endpoints</p></td>
<td></td>
<td></td>
<td><p>AWS PrivateLink, Azure Private Link, GCP Private Service Connect</p></td>
</tr>
<tr>
<td><p>Security logs</p></td>
<td></td>
<td></td>
<td><p><span><i></i></span></p></td>
</tr>
<tr>
<td><p>Single sign-on</p></td>
<td></td>
<td></td>
<td><p><span><i></i></span></p></td>
</tr>
</tbody>
</table>

</div>

<div>

<table>
<caption>Table 5. Pricing and usage</caption>
<colgroup>
<col/>
<col/>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th></th>
<th><span>AuraDB Free</span></th>
<th><span>AuraDB Professional</span></th>
<th><span>AuraDB Enterprise</span></th>
</tr>
</thead>
<tbody>
<tr>
<td><p>Capacity-based consumption pricing model</p></td>
<td></td>
<td><p><span><i></i></span></p></td>
<td><p><span><i></i></span></p></td>
</tr>
<tr>
<td><p>Payment</p></td>
<td></td>
<td><p>Pay-as-you-go with credit card</p></td>
<td><p>Prepaid contract terms with custom pricing</p></td>
</tr>
<tr>
<td><p>Cloud marketplace billing</p></td>
<td></td>
<td><p><span><i></i></span></p></td>
<td><p><span><i></i></span></p></td>
</tr>
<tr>
<td><p>Volume discounts</p></td>
<td></td>
<td></td>
<td><p><span><i></i></span></p></td>
</tr>
<tr>
<td><p>Terms of Service</p></td>
<td><p>Click-through</p></td>
<td><p>Click-through</p></td>
<td><p>Enterprise with commercial negotiations</p></td>
</tr>
<tr>
<td><p>Cloud marketplace private offers</p></td>
<td></td>
<td></td>
<td><p><span><i></i></span></p></td>
</tr>
</tbody>
</table>

</div>

<div>

<div>

<table>
<tbody><tr>
<td>
<i></i>
</td>
<td>
<div>
<p>For information on the different levels of support offered in each plan, see <a>Support</a>.</p>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

</div>

</div>

</div>
