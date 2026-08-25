# Report Generation

## Overview

The report generation phase is the operational output of AWS-Stale-Resource-Analyzer. It translates discovered resource findings into a clear, business-friendly Excel workbook that can be reviewed by engineering, cloud operations, and leadership stakeholders.

The report is designed to support governance and FinOps use cases by presenting:

- A project-level executive summary
- Resource-level findings by service category
- Classification of active, stale, or candidate resources
- Estimated financial impact
- Recommendations for governance action
- Historical context from previous report generations

## Workbook structure

The report includes a set of logical sheets designed to make review and distribution straightforward.

### Executive Summary

This sheet provides the high-level view of the project footprint. It typically includes:

- Project name and tag filter
- Total resources discovered
- Total stale or inactive resources
- Estimated monthly cost impact
- Resource categories with the most waste
- Governance status summary

This page is meant to be the first view for leadership, project owners, and governance reviewers.

### EC2

The EC2 sheet lists resources that match the project tag and are most likely to contribute to waste if idle or underutilized.

Typical fields may include:

- Instance ID
- Name
- Region
- Instance type
- Launch date
- Last activity date
- CPU utilization status
- Estimated monthly cost
- Classification
- Recommendation

### EBS

The EBS sheet surfaces volumes that may be unattached or rarely used.

Typical findings include:

- Unattached volumes
- Low-activity volumes
- Old snapshots or backup artifacts
- Storage costs tied to unnecessary retention
- Recommendation actions such as cleanup or reattachment review

### Lambda

The Lambda sheet focuses on functions with low invocation rates, stale deployments, or unused serverless workloads.

Typical content includes:

- Function name
- Runtime and version
- Last invocation date
- Error rate or execution pattern
- Estimated monthly cost
- Review recommendation

### RDS

This sheet identifies database resources that may be oversized, idle, or no longer required.

Fields may include:

- DB instance identifier
- Engine
- Storage size
- Region
- Last activity date
- Compute cost estimate
- Recommendation

### Security Groups

This view highlights network configuration artifacts that may remain after workloads have been decommissioned.

Typical items include:

- Security group name
- VPC association
- Inbound or outbound rules
- Last observed usage
- Review recommendation

### S3

The S3 sheet identifies buckets or storage objects that may be stale or unnecessarily retained.

Typical review categories include:

- Infrequently accessed buckets
- Long-lived storage with no recent use
- Large retention footprint
- Unused project-specific storage

### IAM

This section helps identify IAM resources or permissions tied to stale workloads, including orphaned role patterns and unused access relationships.

Typical content includes:

- Role or user name
- Last used date
- Project association
- Permission scope
- Governance recommendation

### Snapshots

The snapshots sheet focuses on lifecycle and retention waste. It is a common area for unnecessary cost accumulation.

Typical details include:

- Snapshot ID
- Creation date
- Volume association
- Cost estimate
- Staleness status
- Retention recommendation

## Classification types

The report groups findings into clear governance categories so stakeholders can quickly interpret the result.

### Active

Resources with recent activity and aligned usage patterns.

### Stale

Resources with no meaningful activity within the configured inactivity window.

### At risk

Resources that are not clearly stale but show low usage or incomplete governance alignment.

### Review recommended

Resources that need a human decision due to business-criticality or unclear usage patterns.

### Candidate for decommissioning

Resources that exhibit cost-waste patterns and low operational relevance.

## Estimated savings

A key business value of AWS-Stale-Resource-Analyzer is translating stale resources into a financial estimate. The report provides an estimated savings value for each candidate resource or resource category.

Examples of savings analysis:

- Idle EC2 instance monthly compute cost
- Unattached EBS volume storage cost
- Idle RDS instance cost
- Unused snapshot storage cost
- Legacy security or storage artifacts with no current operational value

These values help leadership and project teams prioritize actionable cleanup work.

## Recommendations

Every report should deliver practical action guidance. Common recommendations include:

- Stop or terminate stale EC2 instances
- Remove unattached EBS volumes
- Decommission unused snapshots
- Review or archive inactive Lambda functions
- Evaluate RDS instances for rightsizing or shutdown
- Reassess storage retention and lifecycle policies
- Validate that old security group rules are still required

## Historical trend visibility

The export is not only a snapshot; it also creates a record of governance history. By storing the output in S3, the organization can compare results over time and track whether resource cleanup is improving.

Historical visibility supports:

- Governance trend analysis
- FinOps review discussions
- Quarterly cleanup tracking
- Project lifecycle accountability
- Auditable cloud hygiene records

## Sample report placeholders

The following placeholders can be used in the repository or documentation while the actual project screenshots are not included.

![Executive Summary Placeholder](https://placehold.co/1400x900/0f172a/ffffff?text=AWS-Stale-Resource-Analyzer+Executive+Summary+Report)

![EC2 Resource Review Placeholder](https://placehold.co/1400x900/1d4ed8/ffffff?text=EC2+Resource+Review)

![Cost and Savings Placeholder](https://placehold.co/1400x900/0f766e/ffffff?text=Estimated+Savings+Summary)

## Storage and naming conventions

Reports are stored in a project-structured S3 path to maintain organization and traceability.

```text
reports/
  Project-TeamX/
    2026/
      08/
        crgr-project-teamx-2026-08-15.xlsx
      09/
        crgr-project-teamx-2026-09-15.xlsx
      10/
        crgr-project-teamx-2026-10-15.xlsx
```

This structure enables:

- Easy retrieval by project and month
- Historical comparison across time periods
- Governance review by business owners
- Archive retention across release cycles

## Report output value

The Excel report provides the operational bridge between raw AWS data and decision-making. It turns a technically complex inventory into a business-ready artifact that project owners and governance teams can review without needing to inspect every AWS service manually.

## Summary

AWS-Stale-Resource-Analyzer's reporting output is designed to be practical, reviewable, and historically valuable. It brings together resource analysis, cost estimation, and governance recommendations in a single contract: the final Excel report. This is the artifact that allows teams to act with evidence and confidence.
