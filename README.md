# Experiments in effect-based I/O prefetching

This repository contains the source code for various experiments with
effect-based I/O prefetching.

## Software

The experiments have been run on different Ubuntu 22.04.2 LTS machines with the following special-purpose software installed.
```
# Installing clang++-17 using https://apt.llvm.org/
$ sudo echo "deb http://apt.llvm.org/jammy/ llvm-toolchain-jammy main" > /etc/apt.d/sources.list.d/llvm-apt.list
$ sudo echo "deb-src http://apt.llvm.org/jammy/ llvm-toolchain-jammy main" >> /etc/apt.d/sources.list.d/llvm-apt.list
# Retrieve key
$ wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key | sudo apt-key add -
# Refresh APT and install clang
$ sudo apt update && sudo install clang-17
# Install libraries
$ sudo apt install libc++1-17 libc++-17-dev libc++abi-17-dev
```

## Hardware

### Machine 1

```
$ lscpu
Architecture:            x86_64
  CPU op-mode(s):        32-bit, 64-bit
  Address sizes:         39 bits physical, 48 bits virtual
  Byte Order:            Little Endian
CPU(s):                  10
  On-line CPU(s) list:   0-9
Vendor ID:               GenuineIntel
  Model name:            Intel(R) Core(TM) i9-10900 CPU @ 2.80GHz
    CPU family:          6
    Model:               165
    Thread(s) per core:  1
    Core(s) per socket:  10
    Socket(s):           1
    Stepping:            5
    CPU max MHz:         2800.0000
    CPU min MHz:         800.0000
    BogoMIPS:            5599.85
    Flags:               fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ss h
                         t tm pbe syscall nx pdpe1gb rdtscp lm constant_tsc art arch_perfmon pebs bts rep_good nopl xtopology nonstop_ts
                         c cpuid aperfmperf pni pclmulqdq dtes64 monitor ds_cpl vmx smx est tm2 ssse3 sdbg fma cx16 xtpr pdcm pcid sse4_
                         1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand lahf_lm abm 3dnowprefetch cpuid_fault
                          epb invpcid_single ssbd ibrs ibpb stibp ibrs_enhanced tpr_shadow vnmi flexpriority ept vpid ept_ad fsgsbase ts
                         c_adjust bmi1 avx2 smep bmi2 erms invpcid mpx rdseed adx smap clflushopt intel_pt xsaveopt xsavec xgetbv1 xsave
                         s dtherm arat pln pts hwp hwp_notify hwp_act_window hwp_epp pku ospke md_clear flush_l1d arch_capabilities
Virtualization features: 
  Virtualization:        VT-x
Caches (sum of all):     
  L1d:                   320 KiB (10 instances)
  L1i:                   320 KiB (10 instances)
  L2:                    2.5 MiB (10 instances)
  L3:                    20 MiB (1 instance)
NUMA:                    
  NUMA node(s):          1
  NUMA node0 CPU(s):     0-9
Vulnerabilities:         
  Itlb multihit:         KVM: Mitigation: VMX disabled
  L1tf:                  Not affected
  Mds:                   Not affected
  Meltdown:              Not affected
  Mmio stale data:       Mitigation; Clear CPU buffers; SMT disabled
  Spec store bypass:     Mitigation; Speculative Store Bypass disabled via prctl and seccomp
  Spectre v1:            Mitigation; usercopy/swapgs barriers and __user pointer sanitization
  Spectre v2:            Mitigation; Enhanced IBRS, IBPB conditional, RSB filling
  Srbds:                 Mitigation; Microcode
  Tsx async abort:       Not affected
```

## References

* G. Nishanov, "Nano-coroutines to the Rescue! (Using Coroutines TS, of Course)", CppCon 2018. [Video](https://www.youtube.com/watch?v=j9tlJAqMV7U).
* C. Jonathan, U. F. Minhas, J. Hunter, J. Levandoski, G. Nishanov, "Exploiting Coroutines to Attack the "Killer Nanoseconds"", VLDB'18. [Paper](https://www.vldb.org/pvldb/vol11/p1702-jonathan.pdf).
