
The following registry keys and values are used to configure the .NET Framework:
1. **SystemDefaultTlsVersions**: Allows the .NET Framework to use the default TLS versions supported by the operating system.
2. **SchUseStrongCrypto**: Enables the use of strong cryptography in the .NET Framework.

## Backing Up the Registry

Before making any changes, it's a good practice to back up the registry keys. Here’s how you can do it using the Command Prompt:

1. **Open Command Prompt as Administrator**:
   - Press `Win + X` and select **Command Prompt (Admin)** or **Windows PowerShell (Admin)** or **Terminal (Admin)**.

2. **Run the Export Commands**: Use the following commands to back up the registry keys. Each command will create a `.reg` file containing the current settings.

    ```sh
    reg export "HKLM\SOFTWARE\Microsoft\.NETFramework\v2.0.50727" "C:\Backup\NETFramework_v2.0.50727.reg"
    reg export "HKLM\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v2.0.50727" "C:\Backup\Wow6432Node_NETFramework_v2.0.50727.reg"
    reg export "HKLM\SOFTWARE\Microsoft\.NETFramework\v4.0.30319" "C:\Backup\NETFramework_v4.0.30319.reg"
    reg export "HKLM\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319" "C:\Backup\Wow6432Node_NETFramework_v4.0.30319.reg"
    ```

    Make sure to replace `"C:\Backup\..."` with the actual path where you want to save the backup files.

3. **Verify the Backup**: Navigate to the backup location and ensure that the `.reg` files have been created.

## Applying the Changes

1. **Open Command Prompt as Administrator**:
   - Press `Win + X` and select **Command Prompt (Admin)** or **Windows PowerShell (Admin)** or **Terminal (Admin)**.

2. **Run the Registry Commands**:
   - Copy and paste each of the following commands into the Command Prompt, pressing `Enter` after each one:

    ```sh
    Reg Add "HKLM\SOFTWARE\Microsoft\.NETFramework\v2.0.50727" /V SystemDefaultTlsVersions /T REG_DWORD /D 0x1 /F
    Reg Add "HKLM\SOFTWARE\Microsoft\.NETFramework\v2.0.50727" /V SchUseStrongCrypto /T REG_DWORD /D 0x1 /F
    Reg Add "HKLM\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v2.0.50727" /V SystemDefaultTlsVersions /T REG_DWORD /D 0x1 /F
    Reg Add "HKLM\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v2.0.50727" /V SchUseStrongCrypto /T REG_DWORD /D 0x1 /F
    Reg Add "HKLM\SOFTWARE\Microsoft\.NETFramework\v4.0.30319" /V SystemDefaultTlsVersions /T REG_DWORD /D 0x1 /F
    Reg Add "HKLM\SOFTWARE\Microsoft\.NETFramework\v4.0.30319" /V SchUseStrongCrypto /T REG_DWORD /D 0x1 /F
    Reg Add "HKLM\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319" /V SystemDefaultTlsVersions /T REG_DWORD /D 0x1 /F
    Reg Add "HKLM\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319" /V SchUseStrongCrypto /T REG_DWORD /D 0x1 /F
    ```

3. **Restart Your Computer**:
   - After running these commands, restart your computer to ensure the changes take effect.

Ref : [Configure for strong cryptography](https://learn.microsoft.com/en-us/mem/configmgr/core/plan-design/security/enable-tls-1-2-client#configure-for-strong-cryptography) & [Transport Layer Security (TLS) best practices with .NET Framework - SystemDefaultTlsVersions](https://learn.microsoft.com/en-us/dotnet/framework/network-programming/tls#systemdefaulttlsversions)
