---
title: Security & Systems Policy
order: 73
description: Learn about Galaxy's Security and Systems Policy
---

<h2 id="galaxy-security">Galaxy's Security Practices</h2>

Galaxy is committed to ensuring that  the application code and data stored in the Meteor Galaxy platform is accessible only by authorized individuals. Security best practices are employed consistently and evolve to meet the needs of our customers.

When you sign up for a Galaxy Account you agree to our standard SLA, found [here](https://galaxy-sla.s3.amazonaws.com/Meteor%2BSoftware%2BLtd.%2B-%2BService%2BLevel%2BAgreement.pdf). If you need a customized SLA for your account, please reach out to support@meteor.com. 


<h2 id="platform-architecture">Platform Architecture</h2>

Galaxy's physical infrastructure is hosted and managed within Amazon's secure data centers and utilize the Amazon Web Service (AWS) technology.

Galaxy consists of Platform services built and run on top of Amazon's Elastic Container Service and Amazon Web Services.

Galaxy utilizes Amazon EC2 virtual machine and Docker isolation mechanisms. Each application instance is run in its own Docker container on an Amazon EC2 virtual machine.

<h2 id="risk-assessments">Risk Assessment</h2>

Amazon continually manages risk and undergoes recurring assessments to ensure compliance with industry standards.

Amazon's data center operations have been accredited under:
- ISO 27001
- SOC 1 and SOC 2/SSAE 16/ISAE 3402 (Previously SAS 70 Type II) PCI Level 1
- FISMA Moderate
- Sarbanes-Oxley (SOX)

Galaxy itself has not pursued independent certifications.

<h2 id="policy-security-updates">Policy around Software Security Updates</h2>

System configuration and consistency is maintained through standard images, configuration management software, and the replacement of select  systems with updated deployments.

Systems are deployed using up-to-date images that are updated with configuration changes and security updates before deployment. Once deployed, existing systems are decommissioned and replaced with up-to-date systems.

<h2 id="customer-data-security">Customer Data Security</h2>

Customer application configuration secrets are stored in a Galaxy system database. This database is secured by standard system and authorization policies. Access to the database is restricted to authorized personnel only, for purposes of administration and support.

Customer application certificates and keys are stored in encrypted form in the Galaxy system database. These certificates are only decrypted on the Galaxy Proxy machines, and are not exposed to application containers.

Access to private information is protected using Docker isolation in the application container.

<h2 id="application-data">Application Data</h2>

Galaxy provides SSL encryption to protect data transmission over the wire from external entities to the Galaxy Proxy layer. Internally in Galaxy, Amazon EC2 virtual machine and Docker container network isolation is utilized to protect data transmission over the wire.

Galaxy does not maintain databases that are utilized for production application use. These databases are provisioned, configured and maintained by the customer.

Galaxy free MongoDB databases are only available for hobby projects and open-source demos. 

<h2 id="application-logs">Application Logs</h2>

Galaxy captures and stores Application Logs in an off-site database. This database is secured by standard system and authorization policies. Access to the database is restricted to authorized personnel for the purposes of administration and support only.

<h2 id="policy-operational">Operational Policies</h2>

Galaxy employees do not access customer data or customer environments as part of day-to-day operations. When customers need support, authorized employees are able to view customer data when specifically requested.

All company employees are trained to understand that customer data privacy and confidentiality is paramount. Under no circumstances is customer data ever disclosed to a third-party. Only a limited subset of employees have the ability to view customer environments and stored data.

Access is routinely evaluated to ensure those rights are retained only when necessary by job function. Galaxy maintains a policy and operational checklist for removing access for employees that are no longer associated with its operations.

<h2 id="two-factor-authentication">Two-Factor Authentication</h2>

Meteor Developer Accounts support Two-Factor Authentication, so we recommend that all members of your organization have it enabled.

You can check if all members of your organization have this enabled in your Members tab on your account page on Galaxy, you will see a lock icon on each member with Two-Factor Authentication enabled. 

Each member can enable Two-Factor Authentication on <a href="https://cloud.meteor.com/security" target="_blank">cloud.meteor.com/security</a> in the Security section.

It's important to save the backup codes in a safe place as well.

<h2 id="dnssec">DNSSEC</h2>
Starting from 22/June/2021, meteor.com is a domain with DNSSEC enabled. Check what DNSSEC is, and why it's important <a href="https://www.icann.org/resources/pages/dnssec-what-is-it-why-important-2019-03-05-en" target="_blank">here</a>. 

<h2 id="changes">Changes</h2>

<h3 id="sep-25-2021">Sep 25th, 2021</h2>

Galaxy applied the following changes to its infrastructure.

- Disable HTTP 1.0 protocol support
- Galaxy Sticky cookie will have a secure flag for force-ssl enabled domains
- HSTS will be sent for every force-ssl enabled domains
- Removal of some supported ciphers. The updated list will only include the ciphers listed below:
  - TLS_AES_128_GCM_SHA256
  - TLS_AES_256_GCM_SHA384
  - TLS_CHACHA20_POLY1305_SHA256
  - TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256
  - TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
  - TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
  - TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
  - TLS_ECDHE_ECDSA_WITH_CHACHA20_POLY1305_SHA256
  - TLS_ECDHE_RSA_WITH_CHACHA20_POLY1305_SHA256
  - TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
  - TLS_RSA_WITH_AES_128_GCM_SHA256
  - TLS_RSA_WITH_AES_128_CBC_SHA

This can affect clients older than 5 years, like old browsers.
