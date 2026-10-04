# Approved Cloud Provider and Topologies for Managed Databases

## 1. Architectural Baseline & Guardrails
* Amazon Web Services (AWS) is the sole approved platform for managed database workloads. Provisioning database engines on alternative public cloud platforms or multi-cloud persistence bridges is strictly prohibited.
* Production workloads must utilize native AWS managed relational solutions (Amazon RDS or Aurora) rather than running unmanaged database software directly on EC2 instances.

## 2. Resource & Topology Matrix
* **Approved Regions:** `us-east-1` and `us-east-2`. Deployments to non-US regions require explicit Cloud Governance Board approval.
* **Network Placement:** Database instances must reside strictly within private database subnets without internet gateway routing.
* **High Availability Baseline:** Production persistence stores must enable Multi-AZ deployment across independent Availability Zones.

## 3. FinOps & Sizing Boundaries
* **Serverless Threshold:** Workloads exhibiting variable or low-throughput patterns (fewer than 50 queries/sec baseline or batch cycles) should default to Aurora Serverless v2 with an auto-scaling cap of 16 ACUs.
* **Provisioned Instance Cap:** Non-production environments must not exceed `db.m6g.xlarge` without an approved capacity justification.
* **Storage Autoscaling:** Storage must use general-purpose SSD (`gp3`) with dynamic storage autoscaling enabled to avoid upfront over-allocation.

## 4. Mandatory Metadata & Attribution (Tagging)
Every database resource definition must include the following tags:
* `Environment`: `dev`, `stage`, or `prod`
* `CostCenter`: Valid corporate billing code format (`CC-[0-9]{4}`)
* `Owner`: Valid team email alias or service identifier
* `DataClassification`: `Confidential`, `Internal`, or `Public`

## 5. Drift & Operational Lifecycle
* **Deletion Protection:** Must be set to `true` for all production database clusters.
* **Snapshot Retention:** Automated retention windows must be set between 7 and 35 days depending on environment classification.
* **Auto-Stop for Dev:** Development instances must support scheduled automated shutdown outside standard business hours.

## 6. Prohibited Topologies & Anti-Patterns
* Deploying relational database engines to public VPC subnets.
* Allocating dedicated IOPS (`io1`/`io2`) in development or staging tiers.
* Declaring non-AWS persistence provider resources (e.g., `google_sql_*`, `azurerm_*`).