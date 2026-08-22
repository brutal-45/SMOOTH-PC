In PowerShell, instead of just typing the drive letter by itself, you have to use the parameter -MountPoint to tell the system which drive you are targeting. 

Here is how those commands look:

## 1. The PowerShell Commands

PowerShell uses a "Verb-Noun" structure, making the commands a bit more readable than the older Command Prompt tools.

**The Command:**

```powershell
Disable-BitLocker -MountPoint "C:"

```

**The Explanation:**

* **`Disable-BitLocker`**: This is the primary action (the Verb-Noun). It tells the Windows operating system to initiate the decryption process and turn BitLocker off completely.
* **`-MountPoint`**: This is a parameter. In Windows architecture, a "mount point" is the gateway through which the operating system accesses a storage volume.
* **`"C:"`**: This is the value you are giving to the `-MountPoint` parameter. It tells PowerShell precisely which mounted drive to target.

**The Command:**

```powershell
Enable-BitLocker -MountPoint "C:" -UsedSpaceOnly

```

**The Explanation:**

* **`Enable-BitLocker`**: Tells Windows to start encrypting the drive to secure it.
* **`-MountPoint "C:"`**: Targets your main C: drive.
* **`-UsedSpaceOnly`**: This is a highly recommended shortcut. Instead of encrypting every single empty byte on a 1-Terabyte hard drive (which can take a whole day), this tells BitLocker to only encrypt the data that actually exists right now. As you create new files later, Windows will encrypt them instantly on the fly.

---

## 2. The Command Prompt (DOS) "Unlock" Commands

These commands are used when a drive is already encrypted, but the door is "locked" (like when you first plug in a BitLocker-protected USB thumb drive). You aren't turning BitLocker off; you are just opening it to see your files.

**The Command:**

```cmd
manage-bde -unlock D: -password

```

**The Explanation:**

* **`manage-bde`**: This calls up the "BitLocker Drive Encryption Configuration Tool," the core engine that handles BitLocker in the background.
* **`-unlock`**: The specific action you want the tool to perform.
* **`D:`**: The target drive. If you plugged in a USB drive, Windows might assign it the letter D, E, or F.
* **`-password`**: This parameter tells the system *how* you intend to unlock it. By typing `-password`, you are telling Windows to prompt you for the standard password you created when you first encrypted the drive.

**The Command:**

```cmd
manage-bde -unlock D: -RecoveryPassword YOUR-48-DIGIT-KEY-HERE

```

**The Explanation:**

* **`-RecoveryPassword`**: This tells Windows that you have forgotten the normal password (or the system is locked down), and you need to use your emergency backup method.
* **`YOUR-48-DIGIT-KEY-HERE`**: This is where you paste the literal 48-digit numerical key that Windows generated for you when you originally set up BitLocker. You type the numbers separated by dashes (e.g., `111111-222222-333333...`).
