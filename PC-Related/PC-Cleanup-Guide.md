# 🧹 Complete PC Cleanup Guide 

Safely remove junk files, optimize storage, and improve system performance.

## ⚡ Quick Cleanup (15 Minutes)

### 1. Disk Cleanup Utility
```powershell
# Run Disk Cleanup as Admin
cleanmgr /sagerun:1

# Or use Storage Sense
start ms-settings:storagesense
```

### 2. Temporary Files Removal
```powershell
# Delete temp files (run as admin)
Remove-Item -Path "$env:TEMP\*" -Recurse -Force -ErrorAction SilentlyContinue
Remove-Item -Path "C:\Windows\Temp\*" -Recurse -Force -ErrorAction SilentlyContinue
```

### 3. Browser Cache Clearing
- **Chrome/Edge**: `Ctrl + Shift + Del` → Select "Cached images" → Clear
- **Firefox**: `Ctrl + Shift + Del` → Choose "Cache" → Clear Now

## 🔍 Deep Clean Operations

### Windows Update Cleanup
```powershell
# Remove old Windows updates (frees GBs of space)
Dism.exe /online /Cleanup-Image /StartComponentCleanup
```

### WinSxS Folder Cleanup
```powershell
# Safe cleanup of component store
Dism.exe /online /Cleanup-Image /SPSuperseded
```

### Prefetch & Superfetch
```powershell
# Clear prefetch (safe to delete)
Remove-Item -Path "C:\Windows\Prefetch\*" -Recurse -Force -ErrorAction SilentlyContinue
```

## 📦 Uninstall Bloatware

### Remove Pre-installed Apps
```powershell
# List all installed apps
Get-AppxPackage | Select Name, PackageFullName

# Remove specific bloatware examples:
Get-AppxPackage *bing* | Remove-AppxPackage
Get-AppxPackage *candycrush* | Remove-AppxPackage
Get-AppxPackage *twitter* | Remove-AppxPackage
Get-AppxPackage *facebook* | Remove-AppxPackage

# Remove OneDrive (if not used)
%SystemRoot%\SysWOW64\OneDriveSetup.exe /uninstall
```

### Common Bloatware to Remove
| Application | Safe to Remove? | Command |
|-------------|----------------|---------|
| Cortana | ✅ Yes | `Get-AppxPackage *Microsoft.549981C3F5F10* \| Remove-AppxPackage` |
| Xbox Game Bar | ⚠️ If not gaming | `Get-AppxPackage *XboxGamingOverlay* \| Remove-AppxPackage` |
| Microsoft Solitaire | ✅ Yes | `Get-AppxPackage *MicrosoftSolitaireCollection* \| Remove-AppxPackage` |
| Skype | ✅ If not used | `Get-AppxPackage *Microsoft.SkypeApp* \| Remove-AppxPackage` |
| Weather/News | ✅ Yes | `Get-AppxPackage *BingWeather* \| Remove-AppxPackage` |

## 💾 Storage Optimization

### Enable Storage Sense
```powershell
# Configure automatic cleanup
Set-ItemProperty -Path "HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion\StorageSense\Parameters\StoragePolicy" -Name "01" -Value 1
```

### Analyze Disk Usage
```powershell
# Check largest folders
Get-ChildItem C:\ -Recurse -ErrorAction SilentlyContinue | 
Where-Object { $_.PSIsContainer } | 
Sort-Object {(Get-ChildItem $_.FullName -ErrorAction SilentlyContinue | Measure-Object -Property Length -Sum).Sum} -Descending | 
Select-Object FullName, @{Name="Size(GB)";Expression={[math]::Round(((Get-ChildItem $_.FullName -ErrorAction SilentlyContinue | Measure-Object -Property Length -Sum).Sum)/1GB,2)}} | 
Select-Object -First 20
```

### Hibernation File (If Not Used)
```powershell
# Disable hibernation (frees ~75% of RAM size)
powercfg /h off

# Re-enable if needed later
# powercfg /h on
```

## 🗑️ Duplicate File Finder

### Using PowerShell
```powershell
# Find duplicate files by hash (example for Downloads folder)
Get-ChildItem "$env:USERPROFILE\Downloads" -File | 
Group-Object Length | 
Where-Object { $_.Count -gt 1 } | 
ForEach-Object { 
    $_.Group | Get-FileHash | Group-Object Hash | Where-Object { $_.Count -gt 1 }
}
```

## 📊 Cleanup Schedule

### Weekly Tasks
- [ ] Clear browser cache
- [ ] Empty Recycle Bin
- [ ] Delete Downloads folder junk

### Monthly Tasks
- [ ] Run Disk Cleanup
- [ ] Review installed programs
- [ ] Clear temporary files
- [ ] Check storage usage

### Quarterly Tasks
- [ ] Deep clean WinSxS
- [ ] Remove unused applications
- [ ] Organize Documents/Pictures
- [ ] Backup important files

## 🛠️ Recommended Cleanup Tools

| Tool | Purpose | Free? | Link |
|------|---------|-------|------|
| **BleachBit** | Deep system cleanup | ✅ Yes | [bleachbit.org](https://www.bleachbit.org/) |
| **TreeSize Free** | Disk space analyzer | ✅ Yes | [jam-software.com](https://www.jam-software.com/treesize_free) |
| **CCleaner** | Registry & file cleanup | ⚠️ Freemium | [ccleaner.com](https://www.ccleaner.com/) |
| **WizTree** | Fast disk visualization | ✅ Yes | [wiztreefree.com](https://wiztreefree.com/) |
| **Duplicate Cleaner** | Find duplicate files | ⚠️ Freemium | [digitalvolcano.co.uk](https://www.digitalvolcano.co.uk/duplicatecleaner.html) |

## ⚠️ Safety Warnings

> ❌ **NEVER DELETE:**
> - `C:\Windows` folder contents
> - `C:\Program Files` or `Program Files (x86)`
> - Files you don't recognize
> - System restore points (unless necessary)

> ✅ **SAFE TO DELETE:**
> - `%TEMP%` folder contents
> - `C:\Windows\Temp` contents
> - Recycle Bin (after verification)
> - Browser cache files
> - Windows.old folder (after 10 days)

## 📈 Performance Impact

Expected results after cleanup:
- **Storage Space**: 5-50 GB freed (varies by usage)
- **Boot Time**: 10-30% faster
- **System Responsiveness**: Noticeable improvement
- **Available RAM**: More free memory

---

> 💡 **Pro Tip**: Create a restore point before major cleanup operations!

> 🔄 **Maintenance**: Set up Storage Sense for automatic cleanup

[← Back to Main README](../README.md)
