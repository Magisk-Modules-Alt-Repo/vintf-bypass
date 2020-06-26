# vintf-bypass
Magisk Module to bypass VTS HAL and Kernel config checks on boot.

# Explanation
From Android 8.0, all Android devices must pass the VTS (Ventor Test Suite) check. It includes a variety of tests including HAL and OS checks.

Each Android device vendor specifies which VINTF (Vendor Interface) object to target, from 1 to 4 (integer). The exact target can be located in `/vendor/etc/vintf/manifest.xml`.

If a Kernel configuration check fails due to a mismatch between the exported `/proc/config.gz` and the specified compatability matrix in `/system/etc/vintf/`, a warning message will appear on every bootup until the configurations match.

# Solution
This module replaces each Kernel configuration check with an empty one, bypassing the VTS checks on boot. It also removes all Vendor HAL checks. The supported Kernel versions that will be bypassed are listed below:

```
- 3.18.0+
- 4.4.0+
- 4.9.0+
- 4.14.0+
- 4.19.0+
- 5.4.0+
- 5.8.0+
```

# Who Is This For
This module is extremely useful for Kernel developers who wish to be creative with their defconfig without succumbing to Google's software mandations. Ideally, custom Kernel users will install this module separately, or bundled with the Kernel flasher, making it entirely universal to bypass. As a result, custom Kernels will no longer require hacky solutions to spoof the output of `/proc/config.gz` (in fact, CONFIG_IKCONFIG can be entirely disabled with this module installed).
