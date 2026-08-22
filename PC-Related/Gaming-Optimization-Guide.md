# 🎮 Gaming Optimization Guide 

Maximize your FPS and reduce input lag with these proven optimization techniques.

## ⚡ Quick Optimizations

### 1. Game Mode Settings
- Press `Win + G` to open Xbox Game Bar
- Enable Game Mode for priority resource allocation
- Disable background recording if not needed

### 2. Graphics Settings
- **NVIDIA Users**: Open NVIDIA Control Panel
  - Set Power Management Mode: "Prefer Maximum Performance"
  - Enable Low Latency Mode: "Ultra"
  - Disable V-Sync for competitive games
  
- **AMD Users**: Open AMD Radeon Software
  - Enable Radeon Anti-Lag
  - Set Texture Filtering Quality: "Performance"
  - Disable Enhanced Sync

### 3. Windows Optimizations
```powershell
# Disable Mouse Acceleration (run as admin in PowerShell)
Set-ItemProperty -Path "HKCU:\Control Panel\Mouse" -Name "MouseSpeed" -Value "0"
Set-ItemProperty -Path "HKCU:\Control Panel\Mouse" -Name "MouseThreshold1" -Value "0"
Set-ItemProperty -Path "HKCU:\Control Panel\Mouse" -Name "MouseThreshold2" -Value "0"
```

### 4. Startup Optimization
- Press `Ctrl + Shift + Esc` to open Task Manager
- Go to Startup tab
- Disable unnecessary applications

### 5. Power Plan
- Press `Win + R`, type `powercfg.cpl`
- Select "High Performance" or create custom plan
- For laptops: Plug in during gaming sessions

## 🔧 Advanced Optimizations

### Disable Fullscreen Optimizations
1. Right-click game executable → Properties
2. Compatibility tab
3. Check "Disable fullscreen optimizations"
4. Click "Change high DPI settings"
5. Check "Override high DPI scaling behavior"

### Priority Settings
1. Launch game
2. `Ctrl + Shift + Esc` → Details tab
3. Right-click game process
4. Set Priority: "High" (NOT Realtime)

## 📊 Monitoring Tools

| Tool | Purpose | Link |
|------|---------|------|
| MSI Afterburner | FPS & Hardware Monitoring | [Download](https://www.msi.com/Landing/afterburner) |
| HWMonitor | Temperature Tracking | [Download](https://www.cpuid.com/softwares/hwmonitor.html) |
| Process Lasso | CPU Priority Automation | [Download](https://bitsum.com/processlasso/) |

## ⚠️ Important Notes

> **Create a restore point before making registry changes!**
> 
> Not all optimizations work for every system. Test each change individually.

## 🎯 Game-Specific Guides

Coming soon:
- Valorant Optimization
- CS2 Settings Guide
- Fortnite Performance Tips
- Apex Legends Configuration

---

**📌 Pro Tip**: Keep your GPU drivers updated for best performance!

[← Back to Main README](../README.md)
