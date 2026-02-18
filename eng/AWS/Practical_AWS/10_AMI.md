# AMI

> A deep dive into AMI - Practical ver.

<br>

<br>

### What is AMI (Amazon Machine Image)?

- A complete **backup** of an EC2 Instance
- Costs are incurred based on the EBS capacity that contains the AMI backup
  - `EBS Volume` has a **Snapshot**
    - A **Snapshot** is a backup of the disk only!
- Snapshots are stored in **S3**
  - Stored in S3 **managed by AWS**
  - They use **incremental backup**
    - Just like docker images...
    - So the second backup is faster!
