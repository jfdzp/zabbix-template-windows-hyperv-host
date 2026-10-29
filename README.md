# Windows Hyper-V Host

Zabbix 7.4 template for Windows Server Hyper-V virtualization hosts, collected
through the Zabbix Agent 2. It is a thin service layer template meant to sit on
top of a general Windows base template: the base template handles CPU, memory,
disk and OS metrics, and this one adds the Hyper-V specific and security
relevant Windows services that must stay running on a hypervisor.

## What it monitors

Each item uses the agent `service.info[<ServiceName>,state]` key, where
`0 = Running` and `6 = Stopped`.

| Service | Key | Severity when stopped |
|---------|-----|-----------------------|
| Hyper-V Host Compute Service | `vmcompute` | Critical |
| Hyper-V Virtual Machine Management | `vmms` | Critical |
| CrowdStrike Falcon (EDR) | `CSFalconService` | Critical |
| Server / SMB file sharing (LanmanServer) | `LanmanServer` | Warning |

## Requirements

- Zabbix Agent 2 installed on the host.
- Linked together with a Windows base template that provides the OS metrics.

## Notes

The service names in the item keys are the real Windows service names. Replace
`CSFalconService` with your own EDR service name if you run a different product,
or remove the item if you do not run one.

## Usage

1. Import `windows_hyperv_host.xml` under Data collection -> Templates.
2. Link it, together with your Windows base template, to the Hyper-V hosts.
