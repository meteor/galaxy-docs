---
title: MongoDB - General
order: 14
description: Information about supported regions, MongoDB versions, types, hardware resources, storage management, disk type, backup policies, logs and metrics, and users for Galaxy Databases.
---

<h2 id="supported-regions">Supported regions</h2>

The Galaxy Databases offer is available in the following regions:

- VIR (Virginia, USA)
- FRA (Frankfurt, Germany)
- SYD (Sydney, Australia)

<h2 id="mongodb-versions">MongoDB versions</h2>

The Galaxy Databases offer supports the following MongoDB versions:

- MongoDB 4.0.19
- MongoDB 4.2.23
- MongoDB 4.4.17
- MongoDB 5.0.14
- MongoDB 6.0.5
- MongoDB 7.0.4

<h2 id="types">Types</h2>

- **Standalone**: A single instance of MongoDB that operates independently. (Standalone does not support Oplog)
- **ReplicaSet**: A set of MongoDB instances that offers high availability and data replication.

<h2 id="hardware-resources">Hardware resources</h2>

Here are the plan types you can choose from:

| Type       | Plan    | RAM    | gCPU  | Storage |
|------------|---------|--------|-------|---------|
| Standalone | Basic   | 512 MB | 0.5   | 5 GB    |
|            | Starter | 1 GB   | 1     | 10 GB   |
|            | Standard| 2 GB   | 2     | 20 GB   |
|            | Pro     | 4 GB   | 4     | 40 GB   |
|            | Plus    | 8 GB   | 6     | 80 GB   |
|            | Ultra   | 16 GB  | 8     | 160 GB  |
|            | Custom  | 32 GB  | 16    | 240 GB  |
| Replicaset | Basic   | 512 MB | 0.5   | 5 GB    |
|            | Starter | 1 GB   | 1     | 10 GB   |
|            | Standard| 2 GB   | 2     | 20 GB   |
|            | Pro     | 4 GB   | 4     | 40 GB   |
|            | Plus    | 8 GB   | 6     | 80 GB   |
|            | Ultra   | 16 GB  | 8     | 160 GB  |
|            | Custom  | 32 GB  | 16    | 240 GB  |

<h2 id="storage-management">Storage Management</h2>

The disk size indicated above represents the total disk capacity of the underlying machine. However, a portion of this capacity is allocated for the operating system installation.

We make concerted efforts to prevent "disk full" scenarios that could jeopardize the health of the cluster. Therefore, the customer will:

- Receive an initial email alert when the cluster's storage capacity reaches 80%.
- Receive a subsequent email alert when the cluster's storage capacity reaches 90%.
- Experience their database instance being transitioned into "read-only" mode once the storage capacity reaches its limit. In this mode, no further write operations can be performed.

<h2 id="disk-type">Disk type</h2>

Here in Galaxy Databases, we use SSD NVMe drives, which are high-performance solid-state drives optimized for rapid data access. They offer low latency and high transfer speeds, making them ideal for applications requiring superior performance.

<h2 id="backup-policies">Backup Policies</h2>

- For **General plan** clusters, automatic daily backups are conducted, with a retention period of 4 days.
- For **Advanced plan** clusters, automatic daily backups are executed, with a retention period of 14 days.
- For **Enterprise plan** clusters, automatic daily backups are performed, with a retention period of 30 days. Here there is the possibility of making a personalized backup and saving it in several different locations.

Contact our team to learn more about Advanced and Enterprise backup plans.

<h2 id="logs-metrics">Logs and Metrics</h2>

Logs and metrics can be accessed through the Galaxy Database. Soon, you will be able to connect your observability tools to capture metrics and logs.

- **Log Retention**: Up to 10,000 lines of logs are retained.
- **Metrics Retention**: Metrics are retained for one calendar month.

Please note that if the database instance is deleted, both logs and metrics are automatically removed.

<h2 id="users">Users</h2>

To effectively manage your MongoDB cluster, the Galaxy Database team sets up several MongoDB users within your clusters:

- **admin@admin**: This is your initial user with administrative privileges.
- **galaxyadmin@admin**: This is a technical user required for automation purposes.
- **galaxybackup@admin**: This user is designated for performing backups.
- **galaxymonitor@admin**: This user is also used for monitoring.