---
layout: page
title: Evasion Framework
description: Testing Android kernel drivers without devices
img: assets/img/evasion.png
importance: 1
category: work
---

<a href="https://github.com/ivanpustogarov/evasion-framework" title="GitHub"><i class="fab fa-github" style="font-size:18px">&nbsp; https://github.com/ivanpustogarov/evasion-framework</i></a>


In this project, we looked at the security of the Android kernel. More
specifically, we looked at the problem of memory corruption vulnerabilities in
various Android kernels and developed a new framework, called EASIER. EASIER
enables a number of powerful dynamic analysis techniques such as coverage-based
fuzzing and symbolic execution for Android kernel device drivers that
ultimately helps in finding such vulnerabilities.

### Android kernel

Operating system kernel, and Android kernel in particular, is the core of
a computer's/smartphone's operating system and generally has complete control over
everything in the system: it controls all hardware resources via device drivers
and manages/controls user-space processes.

Because of this and due to the fact that the Android kernel powers millions of
mobile devices it becomes an attractive target for malicious actors:
vulnerabilities in it are particularly dangerous as they can be exploited by
malicious code to gain high privilege execution level and allow the attacker to
take full control of the vulnerable device.


### Device drivers
The first place to look for kernel vulnerabilities is device driver
code. Since Android devices ship with different peripherals (cameras,
accelerometers, etc.), manufacturers customize the stock Android kernel by adding
corresponding drivers to support those peripherals. As a result, a significant
part of these custom Android kernels consists of driver code that may not be as
rigorously audited as main kernel components.

### Dynamic analysis

Dynamic analysis is a type of program analysis that involves executing program
code and observing its internal state. It is essential for many security tasks
such as exploit development and especially vulnerability detection. Two common
examples of dynamic analysis techniques are coverage-based fuzzing and symbolic
execution. Both of them require fine-grained memory- and CPU-state
introspection. 

When it comes to embedded and mobile devices such as Android smartphones,
achieving such high-resolution code tracing on-device is problematic.  This is not to say
that, on-device analysis would require a smartphone of a particular model for
each analysis instance, which does not scale considering the number of
smartphone devices that exist. This is why we need to use emulation.

### Ex-vivo AnalySIs framEwoRk (EASIER)

Emulated hardware has many benefits, including efficiency, enabling monitoring
that is unavailable on the real hardware and the ability to parallelize and
scale on commodity CPU clusters. Unfortunately, it is challenging to employ
emulation to dynamically analyze device drivers for two reasons. 

#### Hardware and software dependencies

First, drivers have hardware dependencies on proprietary, device-specific
hardware components that are not provided by the current emulators. Unless
these dependencies are satisfied, the drivers will not execute properly in an
emulated environment. Unfortunately, the proprietary nature of the devices
means that their specifications are not available, and while the specifications
can be reverse engineered, the effort required precludes scaling to the
plethora of Android devices that exist. Second, drivers have software
dependencies on the host kernels on which they were meant to run.
Unfortunately, hardware dependencies between the host kernels and the device
hardware also prevent those kernels from running in an emulator. In fact, very
few hardwarespecific kernels can boot on commonly available emulators - for
example, the Qemu emulator only supports a few board-specific kernels.

#### Superficially dependent paths

In this project, we take advantage of the observation that many execution paths
in drivers are only superficially dependent on both the hardware and kernel on
which the driver executes, to create an ex-vivo dynamic driver analysis
framework for Android devices that requires neither porting nor emulation. 

We achieve this by developing a generic evasion framework that enables driver
initialization by evading hardware and kernel dependencies instead of precisely
emulating them, and then developing a novel ex-vivo framework that enables
off-device analysis with the initialized driver state. Compared to on-device
analysis, this approach enables the use of userspace tools and scales with the
number of available commodity CPU’s, not the number of smartphones.
