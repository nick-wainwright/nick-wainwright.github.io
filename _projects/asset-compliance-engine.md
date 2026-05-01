---
layout: project
title: "Asset Compliance Automation Engine"
date: 2024-01-15
description: "Automated CMDB reconciliation system that reduced compliance audit cycle time by 40% across 3,000+ enterprise devices."
tags: [Python, CMDB, Compliance, Automation]
github: "https://github.com/yourusername/asset-compliance-engine"
---

## Overview

Manual asset audits in large enterprise environments are slow, error-prone, and expensive. This project automates the entire CMDB reconciliation workflow — from asset discovery to discrepancy reporting — reducing a 5-day manual audit to a continuous background process.

## Problem Statement

The target organization managed 3,200+ endpoints across 8 physical sites. Annual software license audits required 4–5 person-weeks of manual effort, and discrepancies were frequently missed due to stale CMDB records.

## Solution Architecture

```
Physical Network
      │
      ▼
Discovery Agents (nmap + WMI)
      │
      ▼
Normalization Pipeline
      │
      ▼
CMDB Comparison Engine  ◄──── ServiceNow CMDB API
      │
      ▼
Discrepancy Report (PDF/JSON)
      │
      ▼
JIRA Ticket Auto-creation
```

## Key Components

### Discovery Agent

```python
def scan_network_segment(cidr: str) -> list[Asset]:
    """Discover live hosts and retrieve hardware/software inventory."""
    hosts = nmap_scan(cidr, args="-sV --script=smb-enum-shares")
    assets = []
    for host in hosts:
        assets.append(Asset(
            ip=host.ip,
            hostname=host.hostname,
            os=host.os_match,
            software=wmi_software_inventory(host.ip),
            hardware=wmi_hardware_inventory(host.ip)
        ))
    return assets
```

### Compliance Engine

```python
def verify_asset_compliance(cmdb_records, physical_inventory):
    """
    Validates physical inventory against CMDB.
    Returns list of discrepancies for audit review.
    """
    discrepancies = []
    for asset in physical_inventory:
        if asset.tag not in cmdb_records:
            discrepancies.append({
                'tag': asset.tag,
                'status': 'UNREGISTERED_ASSET',
                'severity': 'HIGH'
            })
        elif not asset.matches(cmdb_records[asset.tag]):
            discrepancies.append({
                'tag': asset.tag,
                'status': 'CONFIGURATION_DRIFT',
                'severity': 'MEDIUM',
                'delta': asset.diff(cmdb_records[asset.tag])
            })
    return discrepancies
```

## Outcomes

- **40% reduction** in audit cycle time (5 days → 3 days)
- **Zero missed discrepancies** in first post-deployment audit
- **Continuous monitoring** rather than point-in-time snapshots
- Integrated with ServiceNow and JIRA for automated ticket creation

## Technologies

Python 3.11, nmap, WMI, ServiceNow REST API, JIRA API, PostgreSQL, Docker
