---
title: "Cara Memperbarui Juju Charm"
description: "Cara mudah memperbarui juju charm pada unit yang sudah berjalan"
date: "2021-08-04"
tags: ["juju", "canonical",  "ubuntu"]
categories: ["juju"]
ShowToc: true
---

# Perintah
```bash
juju refresh [options] <application>
```

# Perbarui ke versi terbaru
```bash
juju refresh <application>
```

* Contoh
```bash
juju refresh prometheus
```

# Perbarui ke versi _revision_ spesifik
```bash
juju refresh --revision <revision number> <application>
```

* Contoh
```bash
juju refresh --revision 22 prometheus
```

# Perbarui ke versi _channel_ spesifik
```bash
juju refresh --channel <channel> <application> 
```

* Contoh
```bash
juju refresh --channel latest/stable prometheus 
```