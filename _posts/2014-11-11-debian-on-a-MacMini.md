---
layout: post
title: Installation de Debian sur un MacMini Intel
---

### Détail du hardware:
	Apple Mac Mini 2.26/2x1G/120/SD/FRA/FRA

	user@machine:~$ lspci
	00:00.0 Host bridge: NVIDIA Corporation MCP79 Host Bridge (rev b1)
	00:00.1 RAM memory: NVIDIA Corporation MCP79 Memory Controller (rev b1)
	00:03.0 ISA bridge: NVIDIA Corporation MCP79 LPC Bridge (rev b2)
	00:03.1 RAM memory: NVIDIA Corporation MCP79 Memory Controller (rev b1)
	00:03.2 SMBus: NVIDIA Corporation MCP79 SMBus (rev b1)
	00:03.3 RAM memory: NVIDIA Corporation MCP79 Memory Controller (rev b1)
	00:03.4 RAM memory: NVIDIA Corporation MCP79 Memory Controller (rev b1)
	00:03.5 Co-processor: NVIDIA Corporation MCP79 Co-processor (rev b1)
	00:04.0 USB controller: NVIDIA Corporation MCP79 OHCI USB 1.1 Controller (rev b1)
	00:04.1 USB controller: NVIDIA Corporation MCP79 EHCI USB 2.0 Controller (rev b1)
	00:06.0 USB controller: NVIDIA Corporation MCP79 OHCI USB 1.1 Controller (rev b1)
	00:06.1 USB controller: NVIDIA Corporation MCP79 EHCI USB 2.0 Controller (rev b1)
	00:08.0 Audio device: NVIDIA Corporation MCP79 High Definition Audio (rev b1)
	00:09.0 PCI bridge: NVIDIA Corporation MCP79 PCI Bridge (rev b1)
	00:0a.0 Ethernet controller: NVIDIA Corporation MCP79 Ethernet (rev b1)
	00:0b.0 SATA controller: NVIDIA Corporation MCP79 AHCI Controller (rev b1)
	00:10.0 PCI bridge: NVIDIA Corporation MCP79 PCI Express Bridge (rev b1)
	00:15.0 PCI bridge: NVIDIA Corporation MCP79 PCI Express Bridge (rev b1)
	00:16.0 PCI bridge: NVIDIA Corporation MCP79 PCI Express Bridge (rev b1)
	02:00.0 VGA compatible controller: NVIDIA Corporation C79 [GeForce 9400] (rev b1)
	03:00.0 Network controller: Broadcom Corporation BCM4321 802.11a/b/g/n (rev 05)
	04:00.0 FireWire (IEEE 1394): LSI Corporation FW643 [TrueFire] PCIe 1394b Controller (rev 07)

	user@machine:~$ cat /proc/cpuinfo
	processor	: 0
	vendor_id	: GenuineIntel
	cpu family	: 6
	model		: 23
	model name	: Intel(R) Core(TM)2 Duo CPU     P8400  @ 2.26GHz
	stepping	: 10
	microcode	: 0xa07
	cpu MHz		: 1596.000
	cache size	: 3072 KB
	physical id	: 0
	siblings	: 2
	core id		: 0
	cpu cores	: 2
	apicid		: 0
	initial apicid	: 0
	fpu		: yes
	fpu_exception	: yes
	cpuid level	: 13
	wp		: yes
	flags		: fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm pbe syscall nx lm constant_tsc arch_perfmon pebs bts rep_good nopl aperfmperf pni dtes64 monitor ds_cpl vmx smx est tm2 ssse3 cx16 xtpr pdcm sse4_1 xsave lahf_lm dtherm tpr_shadow vnmi flexpriority
	bogomips	: 4510.79
	clflush size	: 64
	cache_alignment	: 64
	address sizes	: 36 bits physical, 48 bits virtual
	power management:

	processor	: 1
	vendor_id	: GenuineIntel
	cpu family	: 6
	model		: 23
	model name	: Intel(R) Core(TM)2 Duo CPU     P8400  @ 2.26GHz
	stepping	: 10
	microcode	: 0xa07
	cpu MHz		: 1596.000
	cache size	: 3072 KB
	physical id	: 0
	siblings	: 2
	core id		: 1
	cpu cores	: 2
	apicid		: 1
	initial apicid	: 1
	fpu		: yes
	fpu_exception	: yes
	cpuid level	: 13
	wp		: yes
	flags		: fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm pbe syscall nx lm constant_tsc arch_perfmon pebs bts rep_good nopl aperfmperf pni dtes64 monitor ds_cpl vmx smx est tm2 ssse3 cx16 xtpr pdcm sse4_1 xsave lahf_lm dtherm tpr_shadow vnmi flexpriority
	bogomips	: 4510.63
	clflush size	: 64
	cache_alignment	: 64
	address sizes	: 36 bits physical, 48 bits virtual
	power management:

Boot possible grace a [rEFInd](https://gist.github.com/EmmanuelKasper/9590327#file-efi-boot-on-lenovo-thinkcenter-m92z)

(à suivre...)

