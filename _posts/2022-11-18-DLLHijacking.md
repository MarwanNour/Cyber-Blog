---
layout: post
title: Hijacking DLLs
categories: [Tutorials]
tag: [techniques, windows] 
---


## Overview

Hijacking DLLs has been a very common technique for defense evasion, persistence and privilege escalation on Windows machines. I'll explain and demonstrate two popular techniques used in Windows-targeted malware: DLL Search Order Hijacking and DLL Side-Loading. They are considered to be sub-techniques of the "Hijack Execution Flow" technique (`T1574`) in the MITRE ATT&CK matrix and they are labeled as `T1574.01` and `T1574.02` respectively.

On Linux machines, this translates to Dynamic Linker Hijacking (`T1574.006`) where an attacker would override the `LD_PRELOAD` environment variable. The same concept applies for macOS machines with the `DYLD_INSERT_LIBRARIES` environment variable.

## DLL Search Order Hijacking

As its name suggests, this sub-technique requires the adversary to make use of the DLL search order mechanism to load malicious libraries carrying the same name as the requested libraries required by a program. 

According to Windows documentation, there exists a certain way in which Windows will look for DLLs and it depends on the registry key `HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Session Manager\SafeDllSearchMode`. When its value is set to 1, `SafeDllSearchMode` will be enabled and the search order will the following:

1. DLL Redirection.
2. API sets.
3. SxS manifest redirection.
4. Loaded-module list.
5. Known DLLs.
6. Windows 11, version 21H2 (10.0; Build 22000), and later. The package dependency graph of the process. This is the application's package plus any dependencies specified as `<PackageDependency>` in the `<Dependencies>` section of the application's package manifest. Dependencies are searched in the order they appear in the manifest.
7. The folder from which the application loaded.
8. The system folder. Use the `GetSystemDirectory` function to retrieve the path of this folder.
9. The 16-bit system folder. There's no function that obtains the path of this folder, but it is searched.
10. The Windows folder. Use the `GetWindowsDirectory` function to get the path of this folder.
11. The current folder.
12. The directories that are listed in the `PATH` environment variable. This doesn't include the per-application path specified by the App Paths registry key. The App Paths key isn't used when computing the DLL search path.

When `SafeDllSearchMode` is set to 0 i.e. disabled, the `current folder` moves from position 11 to position 8.

## DLL Side-Loading

TODO: Show difference

## Demo


## Mitigation

TODO


## Conclusion 

TODO

Other DLL techniques (from hacktricks): TODO

## References

- https://attack.mitre.org/techniques/T1574/001
- https://attack.mitre.org/techniques/T1574/002
- https://www.youtube.com/watch?v=3eROsG_WNpE
- https://owasp.org/www-community/attacks/Binary_planting
- https://www.mandiant.com/resources/blog/abusing-dll-misconfigurations
- https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation/dll-hijacking
- https://learn.microsoft.com/en-us/windows/win32/dlls/dynamic-link-library-search-order#standard-search-order-for-unpackaged-apps
- 