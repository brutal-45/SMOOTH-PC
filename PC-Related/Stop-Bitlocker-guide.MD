You have a great memory! You are thinking of the **PowerShell** commands for BitLocker.

In PowerShell, instead of just typing the drive letter by itself, you have to use the parameter `-MountPoint` to tell the system which drive you are targeting.

Here is how those commands look:

## 1. The PowerShell "-MountPoint" Commands

If you are using Windows PowerShell as an Administrator, you use these:

**To turn OFF BitLocker:**

```powershell
Disable-BitLocker -MountPoint "C:"

```

**To turn ON BitLocker:**

```powershell
Enable-BitLocker -MountPoint "C:" -UsedSpaceOnly

```

---

## 2. "Mounting" (Unlocking) a Locked Drive

If you meant "mounting" in the sense of plugging in a locked USB drive and **unlocking** it so you can see your files, you use the `unlock` command.

If you plug in an encrypted drive (like `D:`), you can mount/unlock it via Command Prompt:

**Unlock with a Password:**

```cmd
manage-bde -unlock D: -password

```

*(After you press Enter, it will ask you to type your password. Once entered, the drive will mount and you can use it).*

**Unlock with a Recovery Key:**

```cmd
manage-bde -unlock D: -RecoveryPassword YOUR-48-DIGIT-KEY-HERE

```
