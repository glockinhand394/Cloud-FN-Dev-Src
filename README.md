::: {align="center"}
# Cloud

**A Windows desktop launcher with Fortnite utilities, network tools,
account integration, and system-management services.**

![Platform](https://img.shields.io/badge/platform-Windows%20x64-0078D4?logo=windows)
![.NET](https://img.shields.io/badge/.NET-9.0-512BD4?logo=dotnet)
![UI](https://img.shields.io/badge/UI-WinForms%20%2B%20WebView2-6B4FBB)
![Status](https://img.shields.io/badge/source-decompiled-orange)
:::

> \[!IMPORTANT\] This repository contains **decompiled source code**
> recovered from `Cloud.exe`, not the original developer-authored
> project. Names, comments, formatting, and some project metadata may
> have been lost or transformed. The code has not been independently
> audited or confirmed to build successfully.

------------------------------------------------------------------------

## Contents

-   [Overview](#overview)
-   [Capabilities found in the
    source](#capabilities-found-in-the-source)
-   [Technology](#technology)
-   [Project layout](#project-layout)
-   [Requirements](#requirements)
-   [Build](#build)
-   [Decompilation notes](#decompilation-notes)
-   [Security and responsible use](#security-and-responsible-use)
-   [Disclaimer](#disclaimer)

## Overview

Cloud is a Windows x64 desktop application. The recovered project uses
**.NET 9**, **Windows Forms**, and **Microsoft Edge WebView2** to
provide a desktop shell for a web-based interface.

The source archive includes service classes for Fortnite-related
utilities, DNS and network configuration, proxy management, Discord
integration, application security, settings, logging, and support
reporting.

This README documents components identified in the decompiled files. A
class or method being present does not guarantee that its feature is
enabled, complete, or working in a particular build.

## Capabilities found in the source

### Fortnite and game utilities

  -----------------------------------------------------------------------
  Component                           What the recovered source indicates
  ----------------------------------- -----------------------------------
  `FortniteDetectorService`           Finds a Fortnite installation and
                                      supports setting a custom game
                                      path.

  `FortniteMonitorService`            Monitors Fortnite and includes
                                      process-management methods.

  `FortniteLogService`                Starts and stops live log
                                      monitoring.

  `FortniteResolutionService`         Locates the Fortnite game-user
                                      settings file and contains
                                      resolution-related logic.

  `LobbyBackgroundService`            Detects lobby background states and
                                      imports/applies custom backgrounds.

  `EacPatcherService`                 Contains methods to patch and
                                      restore an Easy Anti-Cheat binary.
                                      Review this code carefully before
                                      use.
  -----------------------------------------------------------------------

### Network and connectivity

  -----------------------------------------------------------------------
  Component                           What the recovered source indicates
  ----------------------------------- -----------------------------------
  `DnsService`                        DNS resolver and DNS enforcement
                                      functionality.

  `DnsBackupService`                  Saves and restores DNS
                                      configuration and includes DNS
                                      hardening methods.

  `NetworkService`                    Network-related operations and
                                      connectivity functionality.

  `ProxyServerService`                Local proxy server implementation.

  `ProxyManagerService`               Starts, stops, and manages proxy
                                      processes and sessions.

  `ProxyOrchestrator`                 Coordinates proxy-related
                                      operations.

  `FirewallService`                   Creates or checks firewall rules.

  `TelemetryBlockerService`           Identifies telemetry domains and
                                      requests and tracks blocked counts.
  -----------------------------------------------------------------------

### Accounts and application services

  -----------------------------------------------------------------------
  Component                           What the recovered source indicates
  ----------------------------------- -----------------------------------
  `DiscordOAuthService`               Discord OAuth flow, PKCE helpers,
                                      token exchange/refresh, user
                                      lookup, and guild-role checking.

  `DiscordRpcService`                 Discord Rich Presence
                                      initialization and updates.

  `KeyValidationService`              Key-format checks and remote
                                      key-validation logic.

  `SupportReportService`              Builds and sends support reports.

  `SettingsService` / `UserSettings`  Loads, saves, resets, and updates
                                      application settings.

  `SecureVault`                       Secure storage-related
                                      functionality.

  `ProtectionService` /               Application protection and security
  `SecurityService`                   checks.

  `CertService`                       Certificate-related checks.

  `FixIssuesService`                  DNS restoration and other repair
                                      operations.

  `FileLogger` / `LoggerService`      Application logging and categorized
                                      log output.
  -----------------------------------------------------------------------

## Technology

The recovered project file (`Cloud.csproj`) identifies the following
configuration:

  Item                   Value
  ---------------------- -------------------------
  Output assembly        `Cloud`
  Target framework       `net9.0-windows7.0`
  Runtime family         .NET 9
  Platform target        x64
  Output type            Windows GUI (`WinExe`)
  Desktop UI             Windows Forms
  Embedded browser       Microsoft Edge WebView2
  C# language version    14.0
  Unsafe code            Enabled
  Application manifest   `app.manifest`
  Application icon       `app.ico`

The project also references framework assemblies including
`System.Management` and WebView2 components. The decompiled project
contains embedded resources with generated-looking filenames.

## Project layout

The main, identifiable source files are arranged approximately as
follows:

``` text
Cloud_extracted/
├── Cloud.csproj
├── app.ico
├── app.manifest
├── CloudLauncherCS/
│   └── MainWindow.cs
├── CloudLauncherCS.Bridge/
│   └── ElectronApiBridge.cs
├── CloudLauncherCS.Services/
│   ├── CertService.cs
│   ├── DiscordOAuthService.cs
│   ├── DiscordRpcService.cs
│   ├── DnsBackupService.cs
│   ├── DnsService.cs
│   ├── EacPatcherService.cs
│   ├── FileLogger.cs
│   ├── FirewallService.cs
│   ├── FixIssuesService.cs
│   ├── FortniteDetectorService.cs
│   ├── FortniteLogService.cs
│   ├── FortniteMonitorService.cs
│   ├── FortniteResolutionService.cs
│   ├── KeyValidationService.cs
│   ├── LobbyBackgroundService.cs
│   ├── LoggerService.cs
│   ├── NetworkService.cs
│   ├── ProtectionService.cs
│   ├── ProxyManagerService.cs
│   ├── ProxyOrchestrator.cs
│   ├── ProxyServerService.cs
│   ├── ResourceExtractor.cs
│   ├── SecureVault.cs
│   ├── SecurityService.cs
│   ├── SettingsService.cs
│   ├── SupportReportService.cs
│   ├── TelemetryBlockerService.cs
│   └── UserSettings.cs
└── [additional decompiled and generated C# files]
```

The archive also contains Visual Studio workspace/cache files under
`.vs/`. These are local IDE artifacts and are not required for a normal
source release.

## Requirements

For development and build attempts:

-   Windows 10 or Windows 11, 64-bit
-   .NET 9 SDK
-   Microsoft Edge WebView2 Runtime
-   Visual Studio 2022 or another IDE that supports the .NET 9 Windows
    Desktop workload (optional)
-   Any external assemblies or resources required by the project

Some services interact with Windows networking, firewall, certificates,
processes, or protected game files. Certain operations may require
elevated permissions. Do not run the application as administrator unless
you have reviewed the relevant code and understand why elevation is
needed.

## Build

Open PowerShell or a terminal in the directory containing
`Cloud.csproj`.

``` powershell
dotnet --info
dotnet restore .\Cloud.csproj
dotnet build .\Cloud.csproj --configuration Release
```

If restore or build fails, inspect the errors before changing the
project.

### Known project-file caveat

The recovered `.csproj` contains explicit assembly references with
absolute paths from the original developer's machine, including paths
into a particular .NET 9 installation. Those paths are unlikely to exist
on another computer.

You may need to replace machine-specific references with supported
framework references or NuGet package references. WebView2 assemblies
and `System.Management` must also be correctly referenced. Because the
source is decompiled and includes obfuscated/generated code, additional
manual fixes may be required.

No successful clean build is claimed by this README.

## Decompilation notes

Decompilation reconstructs source-like code from compiled .NET
Intermediate Language (IL). It does not reproduce the original source
perfectly.

Expect possible differences such as:

-   Missing original comments and documentation.
-   Reconstructed variable names and altered formatting.
-   Compiler-generated async/state-machine code.
-   Obfuscated type, method, and file names.
-   Missing project configuration or development-only files.
-   Embedded resources that are not self-explanatory.
-   Code that requires manual correction before compiling.

Useful tools for inspecting .NET assemblies:

-   [ILSpy](https://github.com/icsharpcode/ILSpy)
-   [dnSpyEx](https://github.com/dnSpyEx)

## Security and responsible use

Review the source before compiling or running it. Pay particular
attention to code that:

-   Changes DNS, firewall, certificate, or other network settings.
-   Starts local proxy services or opens network listeners.
-   Reads or terminates other processes.
-   Modifies Fortnite configuration, game files, or anti-cheat-related
    files.
-   Performs OAuth, key validation, telemetry filtering, or remote
    requests.
-   Stores tokens, credentials, keys, or other sensitive data.

Use a test environment where possible. Back up relevant files and
settings before testing restore, repair, patching, or
configuration-changing features. Only use the software with systems and
accounts you own or are authorized to manage.

## Disclaimer

Cloud and the recovered source are provided here for educational,
interoperability, and code-review purposes. This documentation is based
on names and implementation clues found in the decompiled archive; it is
not a security audit, feature guarantee, or endorsement.

Respect the original developer's rights, applicable software licences,
game terms, and the terms of any third-party services. Do not use the
software to bypass protections, gain unauthorized access, or disrupt
other users' systems.

------------------------------------------------------------------------

::: {align="center"}
**Cloud · Decompiled source documentation**
:::

