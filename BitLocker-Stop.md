Here asking every time bitlocker recovery key when we boot pc , guide to stop this.. 

Ah, that explains exactly what is happening!

When you disable **Secure Boot** in your BIOS/UEFI settings, Windows sees this as a major security environment change. Because BitLocker is designed to protect your data from tampering, it panics, assumes someone is trying to break into the drive, and locks itself down. That is why it demands the 48-digit Recovery Key when you try to switch back to Windows.

To stop this from happening every time you switch operating systems, you have two options.

---

## Option 1: Suspend BitLocker before turning off Secure Boot (Recommended)

If you want to keep your Windows drive encrypted but still want to boot into Linux, you need to tell Windows to "look the other way" before you disable Secure Boot.

1. Boot into Windows (you will have to enter your recovery key this one last time).
2. Click the Start menu, type **PowerShell**, right-click it, and choose **Run as Administrator**.
3. Type this command and press Enter:
```powershell
Suspend-BitLocker -MountPoint "C:"

```


*This puts BitLocker into a temporary "paused" state where it won't check if Secure Boot is on or off.*
4. Restart your PC, go into your BIOS, and disable Secure Boot (or leave it off if it already is).
5. Boot into Linux as much as you want.
6. When you eventually boot back into Windows, open PowerShell as Administrator again and run:
```powershell
Resume-BitLocker -MountPoint "C:"

```


Windows will re-lock itself using the *new* hardware state (with Secure Boot off), and it won't ask you for the key anymore on future boots.

---

## Option 2: Turn off BitLocker permanently

If you plan on dual-booting Linux and Windows frequently and don't want to deal with BitLocker pausing/resuming, your best bet is to just turn it off entirely.

1. Boot into Windows (using your recovery key).
2. Open **PowerShell as an Administrator**.
3. Run the following command:
```powershell
Disable-BitLocker -MountPoint "C:"

```


4. **Important:** Leave your computer powered on and running Windows for a little while. Decrypting the whole drive takes time. You can check the progress by running:
```powershell
Get-BitLockerVolume -MountPoint "C:"

```


Once the **Volume Status** says **FullyDecrypted**, BitLocker is completely gone. You can now turn Secure Boot on or off whenever you want, and Windows will never ask for a recovery key again.

---

### 🔍 Where to find your key if you are stuck right now:

If you are locked out of Windows this exact second and need to get back in to run these commands, use a phone or another computer to log into:
👉 **[windows.microsoft.com/recoverykey](https://windows.microsoft.com/recoverykey)**

Log in with the same Microsoft account you use to sign into your PC, and it will list your 48-digit key.
