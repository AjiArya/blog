---
title: "How To Reset Ceph Admin Dashboard"
description: "Easy way to reset Ceph Admin User on Ceph Dashboard"
date: "2023-07-31"
tags: ["Ceph", "Storage", "Troubleshoot", "Dashboard"]
categories: ["Ceph"]
ShowToc: true
TocOpen: true
---

# Guide
1. Create a file that contain new password
```bash
echo -n "<password>" > dashboard-password
```

2. Update the password
```bash
# Mimic or Older version of ceph
ceph dashboard set-login-credentials admin -i dashboard-password

# Nautilus or Newer version of ceph
ceph dashboard ac-user-set-password admin -i dashboard-password
```

# Referensi
- https://docs.ceph.com/en/mimic/mgr/dashboard/
- https://docs.ceph.com/en/quincy/mgr/dashboard/
