Here is the breakdown of how to turn BitLocker on and off using the Command Prompt, along with an explanation of exactly what the commands do.

*(Remember to run Command Prompt as an **Administrator** for these to work).*

## 1. Turning OFF BitLocker (Decrypting)

**The Command:**

```cmd
manage-bde -off C:

```

**The Explanation:**

* **`manage-bde`**: This is the name of the built-in Windows tool (BitLocker Drive Encryption Configuration Tool). It tells Windows you want to make changes to BitLocker.
* **`-off`**: This is the specific action. It instructs Windows to remove the encryption protection and begin converting the data back to a readable, unencrypted format.
* **`C:`**: This is the target drive. It tells the tool exactly which hard drive to decrypt. You can change this to `D:`, `E:`, etc., if you want to decrypt a USB drive or secondary hard drive.

---

## 2. Turning ON BitLocker (Encrypting)

**The Command:**

```cmd
manage-bde -on C: -usedspaceonly

```

**The Explanation:**

* **`manage-bde`**: The tool used to manage BitLocker.
* **`-on`**: The action telling Windows to start encrypting the drive to secure your data.
* **`C:`**: The target drive you want to encrypt.
* **`-usedspaceonly`** *(Optional but recommended)*: This tells BitLocker to only encrypt the files you currently have on the drive, rather than encrypting the empty, unused space. This makes the encryption process finish much faster. New files will automatically be encrypted as you add them.

> **Important Note for Turning it ON:**
> If you are turning on BitLocker for the `C:` drive via the command line, Windows usually requires you to create a backup "Recovery Key" first so you don't get locked out. If the `-on` command fails, you can generate a recovery password first by running:
> `manage-bde -protectors -add C: -RecoveryPassword`
