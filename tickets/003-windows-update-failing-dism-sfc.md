# TKT-003: Windows Update Failing (repair components + system files)

## Symptoms
- Windows Update fails to install updates (retries or errors out).
- Device may be stuck “Downloading/Installing” or updates repeatedly fail.
- Users report slow performance, reboot loops, or pending restart prompts.

## Environment
- Device/OS: Windows 10/11
- Update mechanism: Windows Update (standard client)

## Triage (what I checked first)
- Confirmed device has stable internet and enough free disk space.
- Checked if a restart was pending (common blocker).
- Reviewed Windows Update history for error codes.

## Diagnostics (commands/logs)
```powershell
# 1) Quick health checks
Get-ComputerInfo | Select-Object WindowsProductName, WindowsVersion, OsHardwareAbstractionLayer

# 2) Check Windows Update service status
Get-Service wuauserv, bits,cryptsvc,msiserver | Select-Object Name, Status, StartType

# 3) Repair Windows image + system files
DISM /Online /Cleanup-Image /RestoreHealth
sfc /scannow

# 4) Windows Update logs (Windows 10/11)
Get-WindowsUpdateLog

# 5) (Optional) View key logs:
# Event Viewer → Applications and Services Logs → Microsoft → Windows → WindowsUpdateClient → Operational
