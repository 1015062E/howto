<br>
<table>
<td>WARNING</td>
<td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td>
</table>
<br>

## Downloading and Setting Up ProcDump

1. **Download ProcDump**:
   - You can download ProcDump from the Sysinternals website - https://docs.microsoft.com/en-us/sysinternals/downloads/procdump

2. **Extract ProcDump**:
   - Extract the downloaded `.zip` file to a folder of your choice.

3. **Open Command Prompt as Administrator**:
   - Navigate to the folder where you extracted ProcDump using the `cd` command.

## Monitoring Exceptions for a Specific PID

To monitor exceptions for a specific process using its Process ID (PID), you can use the following command:

```bash
procdump.exe -accepteula -ma -e -l -f "" <PID>
```

### Command Breakdown:
- `-accepteula`: Automatically accept the EULA.
- `-ma`: Create a full memory dump.
- `-e`: Generate a dump when an unhandled exception occurs.
- `-l`: Capture a dump if the process has a hung window.
- `-f ""`: Filter exceptions based on a string. An empty string means it will capture all exceptions.
- `<PID>`: The Process ID of the process you want to monitor.

### Example:
```bash
procdump.exe -accepteula -ma -e -l -f "" 1234
```

This command will monitor the process with PID 1234 for unhandled exceptions and hung windows, and display any exceptions in the command prompt window.

## Generating a Dump File

If you need to generate a dump file immediately, you can use a simpler command:

```bash
procdump.exe -accepteula -ma <PID> <Dump_Folder>
```

### Example:
```bash
procdump.exe -accepteula -ma 1234 C:\Dumps
```

This command will create a full memory dump of the process with PID 1234 and save it to the `C:\Dumps` folder.

## Important Notes

- **Run as Administrator**: Always run the command prompt as an administrator to ensure ProcDump has the necessary permissions.
- **Disk Space**: ProcDump may require significant disk space to store dump files. Ensure that there is enough disk space available before capturing dumps.

## References

- https://learn.microsoft.com/en-us/sysinternals/downloads/procdump
- https://www.windowscentral.com/how-use-procdump-create-dump-files-windows-10
