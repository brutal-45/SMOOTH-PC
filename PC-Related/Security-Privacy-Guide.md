# 🔒 Windows Security & Privacy Guide 

Essential security configurations to protect your privacy and secure your Windows system.

## 🛡️ Essential Security Steps

### 1. Enable Windows Defender (If Not Using Third-Party)
```powershell
# Check Defender Status
Get-MpComputerStatus

# Enable Real-time Protection
Set-MpPreference -DisableRealtimeMonitoring $false

# Enable Cloud-delivered Protection
Set-MpPreference -MAPSReporting 2
```

### 2. Firewall Configuration
- Press `Win + R`, type `wf.msc`
- Review inbound/outbound rules
- Block suspicious applications
- Enable stealth mode for public networks

### 3. User Account Control (UAC)
- Press `Win + R`, type `UserAccountControlSettings`
- Set to **second from top** (default recommended)
- Never disable completely!

## 🔐 Privacy Settings

### Disable Telemetry
```powershell
# Run as Administrator
reg add "HKLM\SOFTWARE\Policies\Microsoft\Windows\DataCollection" /v AllowTelemetry /t REG_DWORD /d 0 /f

# Disable Diagnostic Tracking Service
Stop-Service DiagTrack -Force
Set-Service DiagTrack -StartupType Disabled
```

### Cortana & Search Privacy
```powershell
# Disable Cortana
reg add "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Search" /v BingSearchEnabled /t REG_DWORD /d 0 /f
reg add "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Search" /v CortanaEnabled /t REG_DWORD /d 0 /f
```

### Location Services
- Settings → Privacy → Location
- Disable for unnecessary apps
- Clear location history

## 🔑 Password & Authentication

### Enable Windows Hello
- Settings → Accounts → Sign-in options
- Set up PIN (more secure than password)
- Configure fingerprint/face recognition if available

### Local Account Best Practices
- Use strong passwords (12+ characters)
- Mix uppercase, lowercase, numbers, symbols
- Enable account lockout policy:
```powershell
net accounts /lockoutthreshold:5 /lockoutduration:30
```

## 🚫 Disable Unnecessary Features

### Remote Desktop (If Not Used)
```powershell
# Disable RDP
reg add "HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server" /v fDenyTSConnections /t REG_DWORD /d 1 /f
```

### SMBv1 (Security Risk)
```powershell
# Disable outdated SMBv1
Disable-WindowsOptionalFeature -Online -FeatureName SMB1Protocol
```

## 📋 Security Checklist

| Task | Status | Priority |
|------|--------|----------|
| ✅ Enable Firewall | ☐ | Critical |
| ✅ Update Windows | ☐ | Critical |
| ✅ Enable Defender/Antivirus | ☐ | Critical |
| ✅ Configure UAC | ☐ | High |
| ✅ Disable Telemetry | ☐ | Medium |
| ✅ Review Startup Apps | ☐ | Medium |
| ✅ Enable BitLocker (if Pro) | ☐ | High |
| ✅ Create Recovery Drive | ☐ | High |

## 🔍 Audit Your System

### Check Running Services
```powershell
# List all running services
Get-Service | Where-Object {$_.Status -eq 'Running'} | Select-Object Name, DisplayName, StartType
```

### Review Installed Software
- Control Panel → Programs → Uninstall
- Remove unused applications
- Check for suspicious entries

### Network Connections
```powershell
# View active connections
netstat -ano

# Find process ID for suspicious connections
Get-Process -Id <PID>
```

## 🆘 Emergency Actions

### If Compromised:
1. Disconnect from internet immediately
2. Boot into Safe Mode with Networking
3. Run full antivirus scan
4. Change all passwords from clean device
5. Check for unauthorized accounts:
```powershell
net user
net localgroup administrators
```

### Reset Windows (Last Resort)
- Settings → Update & Security → Recovery
- Choose "Reset this PC"
- Keep files or remove everything

## 📚 Additional Resources

| Resource | Description |
|----------|-------------|
| [Have I Been Pwned](https://haveibeenpwned.com/) | Check if email is compromised |
| [VirusTotal](https://www.virustotal.com/) | Scan suspicious files |
| [Ninite](https://ninite.com/) | Secure software installer |

---

> ⚠️ **Warning**: Some changes may affect system functionality. Create a restore point first!

> 💡 **Tip**: Regularly update Windows and installed software for latest security patches.

[← Back to Main README](../README.md)
