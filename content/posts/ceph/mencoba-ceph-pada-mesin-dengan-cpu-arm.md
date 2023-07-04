---
title: "Mencoba Ceph Pada Mesin Dengan CPU ARM"
description: "Menunjukkan hasil percobaan deploy Ceph pada mesin dengan CPU ARM"
date: "2023-07-04"
tags: ["Ceph", "Storage", "ARM"]
categories: ["Ceph"]
ShowToc: true
TocOpen: true
---

# Lingkungan
## Spesifikasi Mesin Fisik
- Sistem Operasi: Ubuntu 22.04 LTS
- Sistem Cloud: OpenStack Kolla Yoga
- Server: [GIGABYTE R152-P33](https://www.gigabyte.com/Enterprise/Rack-Server/R152-P33-rev-100) (Disediakan oleh https://imtek.id)
  - 1 x Ampere Computing Ampere Altra Q80-30
  - 4 x 64GB DDR4 3200Mhz
  - 1 x Intel Ethernet Converged Network Adapter X550T
  - 2 x SAMSUNG NVMe SSD 970 EVO Plus 500GB
  - 2 x SAMSUNG NVMe SSD PM9A3 960GB
## Spesifikasi Mesin Virtual
- Sistem Operasi: Ubuntu 22.04 LTS
- Software-defined Storage (SDS): Ceph Quincy
- Detil:

| No | Hostname    | vCPU | Memory | Storage            | Extra Storage        |
|----|-------------|------|--------|--------------------|----------------------|
| 1  | demo-ceph01 | 4    | 8GB    | Disk 1: 50GB (OS)  | Disk 2-4: 50GB (OSD) |
| 2  | demo-ceph02 | 4    | 8GB    | Disk 1: 50GB (OS)  | Disk 2-4: 50GB (OSD) |
| 3  | demo-ceph03 | 4    | 8GB    | Disk 1: 50GB (OS)  | Disk 2-4: 50GB (OSD) |

Berikut merupakan tangkapan layar yang menunjukkan architecture CPU dan informasi sistem operasi
![](/images/mencoba-ceph-pada-mesin-dengan-cpu-arm-image1.jpg)
# Hasil percobaan
## Manual
Berikut merupakan tangkapan layar yang menunjukkan hasil instalasi menggunakan cara manual
![](/images/mencoba-ceph-pada-mesin-dengan-cpu-arm-image2.jpg)

Berikut caranya: [Cara Deploy Ceph Quincy Secara Manual](/posts/ceph/cara-deploy-ceph-secara-manual)

## Cephadm
Berikut merupakan tangkapan layar yang menunjukkan hasil migrasi ceph daemon menjadi cephadm container
![](/images/mencoba-ceph-pada-mesin-dengan-cpu-arm-image3.jpg)

Berikut caranya: [Ceph - Cara Migrasi Ceph Daemon ke cephadm](posts/ceph/cara-migrasi-ceph-daemon-ke-cephadm)

Inspeksi arsitektur container image
![](/images/mencoba-ceph-pada-mesin-dengan-cpu-arm-image4.jpg)

# Referensi
- [Cara Deploy Ceph Quincy Secara Manual](/posts/ceph/cara-deploy-ceph-secara-manual)
- [Ceph - Cara Migrasi Ceph Daemon ke cephadm](posts/ceph/cara-migrasi-ceph-daemon-ke-cephadm)
