# erp-sql-upgrade-2016-to-2019
Security-driven upgrade of Microsoft SQL Server 2016 to 2019 for a mission-critical ERP system. Includes staged dev and production rollout, testing, safeguards, and closure of a Nessus vulnerability.

# SQL Server Upgrade Project: Microsoft SQL Server 2016 to 2019 for ERP System

**Project Owner/Author**: Charlie Hofner
**LinkedIn**: [LinkedIn](https://www.linkedin.com/in/charlie-hofner/)

## Project Overview & Origin

This project was initiated as part of a broader **cybersecurity hardening initiative** following vulnerabilities identified in a Nessus scan.  
The scan flagged SQL Server 2016 as **out of extended support** (extended support ended July 13, 2021, with no further security patches available), creating an unacceptable risk for a mission-critical ERP system.

While several higher-priority vulnerabilities were remediated first, upgrading the ERP SQL instances from 2016 → 2019 was one of the final items closed out in the overall security posture improvement project.

The upgrade affected two environments, both running on **Windows Server 2022**:

- **Development (Dev) Server**: Used for testing and validation.
- **Production (Prod) Server**: Hosted the live ERP database (installed May 2017).

A staged, low-risk rollout was executed: dev first → full validation → production.

### Key Objectives

- Eliminate the unsupported SQL Server 2016 vulnerability.
- Bring the ERP database platform back into a supported lifecycle with security updates.
- Maintain 100% ERP functionality and data integrity.
- Minimize production downtime.

### Timeline

- **November 11, 2024**: Dev server upgrade completed (business hours).
- **November 11–15, 2024**: Intensive post-upgrade testing on dev.
- **November 15, 2024**: Co-worker provided final “all clear” sign-off.
- **November 18, 2024**: Production server upgrade completed after hours.
- **Post-Project**: VMware snapshots removed from both VMs after successful validation and stability confirmation.

**Current Status (December 12, 2025)**: SQL Server 2019 is now in extended support only (mainstream support ended February 2025). Planning for SQL Server 2022+ migration is recommended.

## Approach

Used Microsoft’s supported **in-place upgrade** path (2016 → 2019).

### Prerequisites (Both Servers)

- Updated **Microsoft .NET Framework** to required version (typically 4.8+).
- Installed **Microsoft Visual C++ Redistributable** (2015–2022 packages).

These installations were quick and straightforward.

### Safeguards (Both Environments)

- **VMware Snapshot**: Taken immediately before work began (removed after project completion and stability confirmed).
- **Full SQL Database Backups**: All databases (including master, msdb, model).
- **Post-Upgrade Restart**: Performed to confirm clean service startup.

### Detailed Execution

#### 1. Dev Server – November 11, 2024

- Performed during business hours (dev environment).
- Installed prerequisites → snapshot → backups → in-place upgrade → latest Cumulative Update → restart → validation.
- Post-upgrade tasks: DBCC CHECKDB, statistics updates, index maintenance, connectivity checks.

#### 2. Testing Phase – November 11–15, 2024

- Full ERP regression testing (workflows, reports, integrations).
- Performance monitoring and issue resolution.
- Sign-off received November 15, 2024.

#### 3. Production Server – November 18, 2024 (After Hours)

- Installed prerequisites → snapshot → backups → in-place upgrade → latest Cumulative Update → restart.
- **Total production downtime**: Slightly over one hour.

## Outcomes

- Vulnerability officially closed: No longer running unsupported SQL Server 2016.
- Zero data loss, zero critical incidents.
- Production impact limited to ~1 hour after-hours window.
- Immediate access to security patches and modern features (Intelligent Query Processing, enhanced security, better diagnostics).
- Strong evidence of risk-based prioritization and thorough change management.
- Snapshots safely removed post-project, restoring optimal VM performance and storage efficiency.

## Lessons Learned

- Vulnerability scans (Nessus) are highly effective at driving real remediation when tied to supported-software policies.
- Addressing higher-severity items first is correct prioritization, even if it delays important items like this.
- Dev-first + snapshot + backup strategy delivers near-zero risk for database upgrades.
- Removing snapshots after successful completion follows VMware best practices (reduces storage overhead and potential performance impact).
- Consistent OS versions (Windows Server 2022 on both) simplified prerequisite and compatibility handling.

## Reflection (Charlie Hofner)

This was a textbook example of disciplined, low-risk change management on a critical system. Starting from a security scan finding, prioritizing it appropriately among other vulnerabilities, and executing with strong safeguards (snapshots + backups) ensured zero surprises. The staged approach, explicit testing sign-off, and quick ~1-hour production cutover demonstrated how preparation and coordination pay off. Cleaning up snapshots afterward kept the environment tidy. A solid win for both security and operational stability—exactly the kind of project that strengthens overall IT posture.
