---
title: Security & Systems Policy
order: 53
description: Learn about Galaxy's Security and Systems Policy
---

<h3 id="galaxy-security">Galaxy's Security Practices</h3>

Galaxy is committed to ensuring that  the application code and data stored in the Meteor Galaxy platform is accessible only by authorized individuals. Security best practices are employed consistently and evolve to meet the needs of our customers.

<h3 id="platform-architecture">Platform Architecture</h3>

Galaxy's physical infrastructure is hosted and managed within Amazon's secure data centers and utilize the Amazon Web Service (AWS) technology.

Galaxy consists of Platform services built and run on top of Amazon's Elastic Container Service and Amazon Web Services.

Galaxy utilizes Amazon EC2 virtual machine and Docker isolation mechanisms. Each application instance is run in it's own Docker container on an Amazon EC2 virtual machine.

<h3 id="risk-assessments">Risk Assessments</h3>

Amazon continually manages risk and undergoes recurring assessments to ensure compliance with industry standards.

Amazon's data center operations have been accredited under:
- ISO 27001
- SOC 1 and SOC 2/SSAE 16/ISAE 3402 (Previously SAS 70 Type II) PCI Level 1
- FISMA Moderate
- Sarbanes-Oxley (SOX)

<h3 id="policy-security-updates">Policy around software security updates</h3>

System configuration and consistency is maintained through standard images, configuration management software, and the replacement of select  systems with updated deployments.

Systems are deployed using up-to-date images that are updated with configuration changes and security updates before deployment. Once deployed, existing systems are decommissioned and replaced with up-to-date systems.

<h3 id="customer-data-security">Customer Data Security</h3>

Customer application configuration secrets are stored in a Galaxy system database. This database is secured by standard system and authorization policies. Access to the database is restricted to authorized personnel only, for purposes of administration and support.

Customer application certificates and keys are stored in encrypted form in the Galaxy system database. These certificates are only decrypted on the Galaxy Proxy machines, and are not exposed to application containers.

Access to private information is protected using Docker isolation in the application container.

<h3 id="application-data">Application data</h3>

Galaxy provides SSL encryption to protect data transmission over the wire from external entities to the Galaxy Proxy layer. Internally in Galaxy, Amazon EC2 virtual machine and Docker container network isolation is utilized to protect data transmission over the wire.

Galaxy does not maintain databases that are utilized for application use. These databases are provisioned, configured and maintained by the customer.

<h3 id="application-logs">Application Logs</h3>

Galaxy captures and stores Application Logs in an off-site database. This database is secured by standard system and authorization policies. Access to the database is restricted to authorized personnel for the purposes of administration and support only.

<h3 id="policy-operational">Operational Policies</h3>

Galaxy employees do not access customer data or customer environments as part of Galaxy's day-to-day operations. When customers need support, authorized employees are able to view customer when specifically requested.

All company employees are trained to understand that customer data privacy and confidentiality is paramount. Under no circumstances is customer data ever disclosed to a third-party. Only a limited subset of employees have the ability to view customer environments and stored data.

Access is routinely evaluated to ensure those rights are retained only when necessary by job function. Galaxy maintains a policy and operational checklist for removing access for employees that are no longer associated with its operations.

