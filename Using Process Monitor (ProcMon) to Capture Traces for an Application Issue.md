
# Using Process Monitor (ProcMon) to Capture Traces for an Application Issue

This guide will walk you through the steps to use Process Monitor (ProcMon) to capture traces for an application issue.

## Step 1: Stop(exit) the Application

Before you start capturing traces with ProcMon, make sure to stop(exit) the application that is having the issue.

## Step 2: Download ProcMon

You can download the latest version of ProcMon from the [Microsoft Sysinternals website](https://docs.microsoft.com/en-us/sysinternals/downloads/procmon) or directly use this link https://download.sysinternals.com/files/ProcessMonitor.zip

## Step 3: Run ProcMon

After downloading and extracting the ProcMon files, run the `Procmon.exe` file as an administrator.

## Step 4: Reproduce the Issue

With ProcMon running, reproduce the issue you are experiencing with the application. ProcMon will automatically start capturing traces.

## Step 5: Stop Collecting Traces

Once you have reproduced the issue, stop collecting traces by clicking on the `Capture` button in the toolbar or by pressing `Ctrl+E`.
<br>![image](https://github.com/guoqingsun-msft/guoqingsun/assets/85205970/0207e785-daaf-4661-bde9-ef8649bc8b3a)<br>

## Step 6: Save the Trace

Save the trace by going to `File > Save` and selecting a location to save the trace file. (Note down the location else you might forget where it was saved)
<br>![image](https://github.com/guoqingsun-msft/guoqingsun/assets/85205970/189c55cf-7096-4cff-92aa-74aab51e21d6)<br>

## Step 7: Compress and Upload the Trace

**Compress** the trace file and then upload it to the workspace shared with you for uploading files.
<br>![image](https://github.com/guoqingsun-msft/guoqingsun/assets/85205970/c93b2bad-c0c2-44a7-a6be-4bd44db38c7b)<br>

<br>If you have any questions or need further assistance, feel free to ask.
