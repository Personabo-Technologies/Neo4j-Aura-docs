<div>

<div>

# Security

</div>

<div>

## Encryption

<div>

<div>

All data stored in Neo4j Aura is encrypted using intra-cluster
encryption between the various nodes comprising your database and
encrypted at rest using the underlying cloud provider's encryption
mechanism.

</div>

<div>

By default, Google Cloud and AWS encrypt all backup buckets (including
the objects stored inside) with either Google-managed encryption or AWS
SSE-S3 encryption.

</div>

</div>

</div>

<div>

## VPC isolation

<div>

<div>

AuraDB Enterprise AuraDS Enterprise

</div>

<div>

AuraDB Enterprise and AuraDS Enterprise run within a Virtual Private
Cloud (VPC) isolation for your deployment.

</div>

<div>

The VPC enables you to operate within an isolated section of the
service, where your processing, networking, and storage are further
protected.

</div>

<div>

Please note that the Aura console runs in a separate VPC.

</div>

<div>

### AWS Private endpoints

<div>

AuraDB Enterprise

</div>

<div>

AuraDB Enterprise supports private endpoints on AWS using AWS
PrivateLink.

</div>

<div>

Once activated, you can create an endpoint in your VPC that connects to
Aura.

</div>

<div>

<div>

</div>

<div>

Figure 1. VPC connectivity with AWS PrivateLink

</div>

</div>

<div>

All applications running Neo4j workloads inside the VPC are routed
directly to your isolated environment in Aura without traversing the
public internet. You can then disable public traffic, ensuring all
traffic to the database remains private to your VPC.

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
<ul>
<li>
<p>When activated, PrivateLink applies to all databases in the region.</p>
</li>
<li>
<p>If you disable public traffic, you must use a dedicated VPN to connect to your database via Browser or Bloom.</p>
</li>
<li>
<p>Connections using private endpoints are one-way. Aura VPCs can’t initiate connections back to your VPCs.</p>
</li>
<li>
<p>In AWS region us-east-1, we do not support the Availability Zone with ID use1-az3 for private endpoints.</p>
</li>
</ul>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

<div>

#### Browser and Bloom access over private endpoints

<div>

To connect to your database via Browser or Bloom, you must use a
dedicated VPN. This is because when you disable public access to your
database, this applies to all connections, including those from your
computer when using Browser or Bloom.

</div>

<div>

Without private endpoints, you access Browser and Bloom over the
internet:

</div>

<div>

<div>

</div>

<div>

Figure 2. Architecture overview before enabling private endpoints

</div>

</div>

<div>

When you have enabled private endpoints **and** disabled public internet
access, you can no longer connect Browser or Bloom to your databases
over the internet:

</div>

<div>

<div>

</div>

<div>

Figure 3. Architecture overview with private endpoints enabled and
public traffic disabled

</div>

</div>

<div>

To continue accessing Browser and Bloom, you can configure a VPN
(Virtual Private Network) in your VPC and connect to Browser and Bloom
over the VPN.

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
<p>To access Bloom and Browser over a VPN, you must ensure that:</p>
</div>
<div>
<ul>
<li>
<p>The VPN server uses the <a>VPC’s DNS servers</a>.</p>
</li>
<li>
<p>You use the private URL provided by support when you completed setting up the private endpoint. It will be different from the URL you used before.</p>
</li>
</ul>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

<div>

<div>

</div>

<div>

Figure 4. Accessing Browser and Bloom over a VPN

</div>

</div>

</div>

<div>

#### Enabling private endpoints

<div>

To enable private endpoints using AWS PrivateLink, please raise a
support ticket, and we'll be in touch.

</div>

<div>

You will need an AWS account with permissions to create, modify,
describe and delete endpoints. Please see the AWS Documentation for more
information.

</div>

</div>

</div>

<div>

### GCP Private endpoints

<div>

AuraDB Enterprise AuraDS Enterprise

</div>

<div>

Aura Enterprise supports private endpoints on GCP using GCP Private
Service Connect.

</div>

<div>

Once activated, you can create an endpoint in your VPC that connects to
Aura.

</div>

<div>

<div>

</div>

<div>

Figure 5. VPC connectivity with GCP Private Service Connect

</div>

</div>

<div>

All applications running Neo4j workloads inside the VPC are routed
directly to your isolated environment in Aura without traversing the
public internet. You can then disable public traffic, ensuring all
traffic to the database remains private to your VPC.

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
<ul>
<li>
<p>When activated, Private Service Connect applies to all databases in the region.</p>
</li>
<li>
<p>If you disable public traffic, you must use a dedicated VPN to connect to your database via Browser or Bloom.</p>
</li>
<li>
<p>Connections using private endpoints are one-way. Aura VPCs can’t initiate connections back to your VPCs.</p>
</li>
</ul>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

<div>

#### Browser and Bloom access over private endpoints

<div>

To connect to your database via Browser or Bloom, you must use a
dedicated VPN. This is because when you disable public access to your
database, this applies to all connections, including those from your
computer when using Browser or Bloom.

</div>

<div>

Without private endpoints, you access Browser and Bloom over the
internet:

</div>

<div>

<div>

</div>

<div>

Figure 6. Architecture overview before enabling private endpoints

</div>

</div>

<div>

When you have enabled private endpoints and disabled public internet
access, you can no longer connect Browser or Bloom to your databases
over the internet:

</div>

<div>

<div>

</div>

<div>

Figure 7. Architecture overview with private endpoints enabled and
public traffic disabled

</div>

</div>

<div>

To continue accessing Browser and Bloom, you can configure a GCP Cloud
VPN (Virtual Private Network) in your VPC and connect to Browser and
Bloom over the VPN.

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
<p>To access Bloom and Browser over a VPN, you must ensure that:</p>
</div>
<div>
<ul>
<li>
<p>You have setup <a>GCP Cloud DNS</a>, or an equivalent DNS service, inside of the VPC.</p>
</li>
<li>
<p>You use the private URL provided by support when you completed setting up the private endpoint. It will be different from the URL you used before.</p>
</li>
</ul>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

<div>

<div>

</div>

<div>

Figure 8. Accessing Browser and Bloom over a VPN

</div>

</div>

</div>

<div>

#### Enabling private endpoints

<div>

To enable private endpoints using GCP Private Service Connect, please
raise a support ticket, and we'll be in touch.

</div>

<div>

Please see the GCP Documentation for required roles and permissions.

</div>

</div>

</div>

<div>

### Azure Private endpoints

<div>

AuraDB Enterprise

</div>

<div>

Aura Enterprise supports private endpoints on Azure using Azure Private
Link.

</div>

<div>

Once activated, you can create an endpoint in your Virtual Network
(VNet) that connects to Aura.

</div>

<div>

<div>

</div>

<div>

Figure 9. VNet connectivity with Azure Private Link

</div>

</div>

<div>

All applications running Neo4j workloads inside the VNet are routed
directly to your isolated environment in Aura without traversing the
public internet. You can then disable public traffic, ensuring all
traffic to the database remains private to your VNet.

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
<ul>
<li>
<p>When activated, Private Link applies to all databases in the region.</p>
</li>
<li>
<p>If you disable public traffic, you must use a dedicated VPN to connect to your database via Browser or Bloom.</p>
</li>
<li>
<p>Connections using private endpoints are one-way. Aura VNets can’t initiate connections back to your VNets.</p>
</li>
</ul>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

<div>

#### Browser and Bloom access over private endpoints

<div>

To connect to your database via Browser or Bloom, you must use a
dedicated VPN. This is because when you disable public access to your
database, this applies to all connections, including those from your
computer when using Browser or Bloom.

</div>

<div>

Without private endpoints, you access Browser and Bloom over the
internet:

</div>

<div>

<div>

</div>

<div>

Figure 10. Architecture overview before enabling private endpoints

</div>

</div>

<div>

When you have enabled private endpoints and disabled public internet
access, you can no longer connect Browser or Bloom to your databases
over the internet:

</div>

<div>

<div>

</div>

<div>

Figure 11. Architecture overview with private endpoints enabled and
public traffic disabled

</div>

</div>

<div>

To continue accessing Browser and Bloom, you can configure a VPN
(Virtual Private Network) in your VNet and connect to Browser and Bloom
over the VPN.

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
<p>To access Bloom and Browser over a VPN, you must ensure that:</p>
</div>
<div>
<ul>
<li>
<p>You have setup <a>Azure Private DNS</a>, or an equivalent DNS service, inside of the VNet.</p>
</li>
<li>
<p>You use the private URL provided by support when you completed setting up the private endpoint. It will be different from the URL you used before.</p>
</li>
</ul>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

<div>

<div>

</div>

<div>

Figure 12. Accessing Browser and Bloom over a VPN

</div>

</div>

</div>

<div>

#### Enabling private endpoints

<div>

To enable private endpoints using Azure Private Link, please raise a
support ticket, and we'll be in touch.

</div>

<div>

Please see the Azure Documentation for required roles and permissions.

</div>

</div>

</div>

</div>

</div>

<div>

## Single Sign-On

<div>

<div>

AuraDB Enterprise AuraDS Enterprise

</div>

<div>

AuraDB Enterprise supports Single Sign-On (SSO) for accessing the Bloom
and Browser clients.

</div>

<div>

The following OpenID Connect (OIDC) certified Identity Providers (IdPs)
are currently supported:

</div>

<div>

-   Microsoft Azure Active Directory (AAD)

-   Okta

-   Keycloak

-   Google Authentication

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
<p>If the IdP you are currently using is not in our list of certified IdPs above, please let us know using the support ticket method mentioned below and we will evaluate the possibility of adding support.</p>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

<div>

Aura supports Authorization Code Flow with PKCE to ensure best practice
security.

</div>

<div>

To add SSO for Browser and Bloom to your AuraDB Enterprise databases,
please raise a support ticket including the following information:

</div>

<div>

1.  The **Connection URI** of the database(s) you want to use SSO.

2.  Whether or not you want Browser, Bloom, or both enabled.

3.  The name of your IdP.

4.  Confirmation that the authorization flow is PKCE.

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
<p>If you have to specify an application type when configuring your client, Neo4j is a Single-page application.
For more information on configuring your client, see <a>Neo4j Single Sign-On (SSO) Configuration</a>.</p>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

</div>

</div>

<div>

## Supported TLS cipher suites

<div>

<div>

For additional security, client communications are carried via TLS v1.2
and TLS v1.3.

</div>

<div>

AuraDB has a restricted list of cipher suites accepted during the TLS
handshake, and does not accept all of the available cipher suites. The
following list conforms to safety recommendations from IANA, the
OpenSSL, and GnuTLS library.

</div>

<div>

TLS v1.3:

</div>

<div>

-   `TLS_CHACHA20_POLY1305_SHA256 (RFC8446)`

-   `TLS_AES_128_GCM_SHA256 (RFC8446)`

-   `TLS_AES_256_GCM_SHA384 (RFC8446)`

</div>

<div>

TLS v1.2:

</div>

<div>

-   `TLS_DHE_RSA_WITH_AES_128_GCM_SHA256 (RFC5288)`

-   `TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 (RFC5289)`

-   `TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384 (RFC5289)`

-   `TLS_ECDHE_RSA_WITH_CHACHA20_POLY1305_SHA256 (RFC7905)`

-   `TLS_DHE_RSA_WITH_AES_256_GCM_SHA384 (RFC5288)`

</div>

</div>

</div>

</div>
