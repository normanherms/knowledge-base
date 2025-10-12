# Lernressourcen-Sammlung (frei & verifiziert)

Diese Sammlung enthält frei zugängliche Lernressourcen (Videos, Blogs, Podcasts, PDFs), die ich persönlich hilfreich finde.
Alle Links wurden auf Zugänglichkeit geprüft, die Verantwortung für die Inhalte liegt bei den jeweiligen Anbietern.

---

## Level 0 – KVM & Libvirt (Virtualisierung verstehen)

**Videos:**

* [QEMU/KVM for absolute beginners (YouTube)](https://www.youtube.com/watch?v=BgZHbCDFODk) – einfacher Einstieg mit visueller Erklärung
* [QEMU/KVM & Libvirt für Einsteiger (Deutsch)](https://youtu.be/37r9dJ_5xgk) – Schritt-für-Schritt-Anleitung für deine erste VM
* [KVM and Virt Manager Install and Setup Guide](https://www.youtube.com/watch?v=rXNjOrFiNtA)

**Artikel & Dokus:**

* [Virtualization Using KVM + QEMU + Libvirt (dwarmstrong.org)](https://www.dwarmstrong.org/kvm-qemu-libvirt/)
* [Virtualization on Linux using KVM/QEMU/Libvirt stack (Bitgrounds)](https://bitgrounds.tech/posts/kvm-qemu-libvirt-virtualization/)
* [Walk‑through using QEMU/KVM with libvirt on Ubuntu (libvirt.org)](https://wiki.libvirt.org/UbuntuKVMWalkthrough.html)
* [Getting Started With KVM (Baeldung)](https://www.baeldung.com/linux/kernel-based-virtual-machine)
* [QEMU / KVM Virtual Machines (Proxmox Wiki)](https://pve.proxmox.com/wiki/Qemu/KVM_Virtual_Machines)

**Podcast-Tipp:**

* [Linux Unplugged #518 – “Virtualization Made Easy”](https://linuxunplugged.com/518) – lockere Einführung in Virtualisierungskonzepte

---

## Level 1 – Fundament (Linux-Isolation)

**Artikel & Blogs:**

* [Learning Containers From The Bottom Up (iximiuz)](https://iximiuz.com/en/posts/container-learning-path/)
* [Linux namespaces in practice (Red Hat Blog)](https://www.redhat.com/sysadmin/7-linux-namespaces)
* [Deep Dive into cgroups v2 (systemd.io)](https://systemd.io/CGROUPS/) – offizieller systemd-Artikel

**Video:**

* [Containers From Scratch (Liz Rice, YouTube)](https://www.youtube.com/watch?v=8fi7uSYlOdc) – Klassiker zur Container-Isolation

**Podcast:**

* [Command Line Heroes S4E2 – “The Containers That Run the World”](https://www.redhat.com/en/command-line-heroes/season-4/the-containers-that-run-the-world)
* [Focus on Linux – "systemctl hibernate"](https://podcasts.apple.com/us/podcast/focus-on-linux/id1606139089) – systemctl und Energieverwaltung unter Linux

---

## Level 2 – containerd & nerdctl

**Artikel & Tutorials:**

* [Getting started with containerd (Moby Blog)](https://blog.mobyproject.org/getting-started-with-containerd-a81fa090982f)
* [Why containerd Was Created: A Complete Setup Guide (Medium)](https://thamizhelango.medium.com/why-containerd-was-created-a-complete-setup-and-tutorial-guide-7a51781ea843)
* [Installing and Configuring containerd as a Kubernetes Container Runtime (Nocentino Blog)](https://www.nocentino.com/posts/2021-12-27-installing-and-configuring-containerd-as-a-kubernetes-container-runtime/)
* [Containerd runtime options for Kubernetes (kubernetes.io)](https://kubernetes.io/blog/2017/11/containerd-container-runtime-options-kubernetes/)
* [Getting Started with nerdctl (Earthly Blog)](https://earthly.dev/blog/nerdctl/)
* [A Comprehensive Guide to Native Management Tools in 2025 (AlphaBravo)](https://blog.alphabravo.io/mastering-containerd-a-comprehensive-guide-to-native-management-tools-in-2025/)
* [Containerd vs Docker: Runtime Comparison (Spacelift)](https://spacelift.io/blog/containerd-vs-docker)
* [Hello nerdctl (Medium)](https://medium.com/@salimwp/hello-nerdctl-16347cc194ff)

**Video:**

* [containerd Explained (TechWorld with Nana)](https://www.youtube.com/watch?v=sK5i-N34im8)

---

## Level 3 – Infrastruktur-Automation

**Terraform:**

* [Terraform Getting Started Guide (HashiCorp Docs)](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)
* [Libvirt Provider Examples (GitHub)](https://github.com/dmacvicar/terraform-provider-libvirt/tree/main/examples)

**Ansible:**

* [Ansible Basics (Red Hat Official)](https://www.redhat.com/en/topics/automation/learning-ansible-tutorial)
* [Ansible Playbooks Explained (DigitalOcean)](https://www.digitalocean.com/community/tutorial_series/getting-started-with-ansible)

**Video:**

* [Terraform vs Ansible: IaC Explained (TechWorld with Nana)](https://www.youtube.com/watch?v=l4r0IXjAlpc)

**Podcast:**

* [Focus on Linux – CfgMgmtCamp 2025](https://podcasts.apple.com/us/podcast/focus-on-linux/id1606139089) – Puppet, OpenTofu, PKL – aktuelle Tools für Konfigurationsmanagement

---

## Level 4 – KubeVirt (Hybrid-Virtualisierung)

**Offizielle Ressourcen / Dokumente:**

* [KubeVirt Quickstart Guide](https://kubevirt.io/quickstart_minikube/)
* [KubeVirt User Guide (Docs)](https://kubevirt.io/user-guide/)
* [KubeVirt: How to Run VMs on Kubernetes (Platform9, PDF)](https://platform9.com/media/KubeVirt-How-to-Run-VMs-on-Kubernetes.pdf)
* [Using KubeVirt on SUSE Linux Enterprise (PDF)](https://documentation.suse.com/sles/15-SP7/pdf/article-kubevirt_en.pdf)
* [Simplifying KubeVirt – New Tools for Easier VM Management (FOSDEM 2025 PDF)](https://archive.fosdem.org/2025/events/attachments/fosdem-2025-5121-simplifying-kubevirt-new-tools-for-easier-vm-management/slides/238618/fosdem202_PXhPPOM.pdf)
* [KubeVirt Module (Oracle Cloud Native Environment PDF)](https://docs.oracle.com/cd/F33069_01/1.7/kubevirt/OCNE-1-7-KUBEVIRT.pdf)
* [KubeVirt Vortrag (Linux Foundation)](https://events19.linuxfoundation.org/wp-content/uploads/2017/11/KubeVirt-Cats-and-Dogs-Living-Together-Stephen-Gordon-Red-Hat.pdf)

**Tutorials & Blogposts:**

* [A Working KubeVirt Tutorial (WWT Blog)](https://www.wwt.com/blog/a-working-kubevirt-tutorial)

**Video:**

* [Running VMs on Kubernetes with KubeVirt (YouTube – The Linux Foundation)](https://www.youtube.com/watch?v=9MZtYV9mGxg)

**Podcast:**

* [Focus on Linux – SUSECON 2025 (Teil 1+2)](https://podcasts.apple.com/us/podcast/focus-on-linux/id1606139089) – Rancher, Uyuni, ARM, Hybrid-Virtualisierung

---

## Level 5 – K3s & Orchestrierung

(... bleibt gleich ...)

---

## Level 6 – DockSeed Production (Monitoring, Backup, Security)

(... vorhandene Inhalte ...)

**Weitere Tools:**

* [Checkmk (Open Source Monitoring)](https://checkmk.com/de) – performantes Monitoring mit Web-Oberfläche
* [BorgBackup Dokumentation](https://www.borgbackup.org/) – verschlüsseltes, deduplizierendes Backup
* [Rsync Manpage (linux.die.net)](https://linux.die.net/man/1/rsync)

**Podcast:**

* [Focus on Linux – Newsupdate 01/25](https://podcasts.apple.com/us/podcast/focus-on-linux/id1606139089) – Rsync-CVE, Proxmox, Kernel-Update, OpenCloud
* [Focus on Linux – Newsupdate 03/25](https://podcasts.apple.com/us/podcast/focus-on-linux/id1606139089) – Proxmox, OpenCloud, Hardware, Framework

---

## Level 7 – DevOps Essentials (Helm, GitOps, CI/CD)

(... vorhandene Inhalte ...)

**Podcast (deutsch):**

* [Focus on DevOps – Secret Management](https://podcasts.apple.com/de/podcast/focus-on-devops/id1542623849) – Token, Zertifikate, Vault-Strategien in DevOps-Pipelines
* [Focus on DevOps – Newsfolge 03/2024](https://focus.sva.de/podcast/focus-on-devops-newsfolge-03-2024/) – Kubernetes, CNCF Landscape, Trends

---

## Begleitmodule

**Netzwerk & Security:**

* [WireGuard Official Docs](https://www.wireguard.com/quickstart/)
* [nftables Introduction (Netfilter Project)](https://wiki.nftables.org/wiki-nftables/index.php/Main_Page)

**Storage & Backup:**

* [Ceph Architecture Overview](https://docs.ceph.com/en/latest/architecture/)
* [MinIO Quickstart](https://min.io/docs/minio/linux/index.html)

**Monitoring:**

* [Prometheus Getting Started](https://prometheus.io/docs/introduction/overview/)
* [Loki + Promtail Setup (Grafana)](https://grafana.com/docs/loki/latest/)

## Konferenzen & aktuelle Praxisbeispiele

* [ContainerDays 2025 (YouTube-Playlist)](https://www.youtube.com/playlist?list=PLHhKcdBlprMcXioPQP4QVF7p16kayKUF5) – Vorträge, Use-Cases und Trends rund um Container, Kubernetes und DevOps

---

*Alle Links geprüft am 2025‑10‑12. Nur frei zugängliche, werbefreie Quellen wurden aufgenommen.*
