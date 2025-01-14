# How to Capture Computer Performance Traces via CMD

This guide will show you how to capture computer performance traces using the `logman` command in the Command Prompt (CMD). For more information about the `logman` command, please refer to the [official documentation](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/logman).

## Step 1: Create a Folder for Perfmon Traces

First, create a folder to hold the perfmon traces. For example, you can create a folder named `C:\PerfMonLogs\`. You can also change the destination folder accordingly by modifying the path in the first command below.

## Step 2: Create a Counter

Run the Command Prompt (CMD) as an administrator and execute the following commands. This step creates a counter, but it does not run without running the "start" command in step 3.

```cmd
logman create counter msperf -f bin -c "\LogicalDisk(*)\*" "\PhysicalDisk(*)\*" "\Processor(*)\*" "\Process(*)\*" "\Memory\*" "\System\*" "\HTTP Service\*" "\HTTP Service Request Queues(*)\*" "\HTTP Service Url Groups(*)\*" -si 00:00:01 -o C:\PerfMonLogs\MS_perf_log.blg -cnf 24:00:00 -max 64
```

## Step 3: Start Capturing

Start capturing by running the following command. Reproduce your issue after this step and before step 4.

```cmd
logman start msperf
```

**Note:** Reproduce your issue now after running the above "start" command (or monitor the issue closely if it happens intermittently and cannot be forecasted when it will occur again next time).

## Step 4: Stop Collecting

Stop collecting by running the following command after reproducing the issue. You can find the log from the specified folder in your first command (e.g., `C:\PerfMonLogs\`).

```cmd
logman stop msperf
```

## Step 5: Delete the Counter

Delete the counter created in step 2 by running the following command. You can also leave it if it has already stopped, as it does not cause any impact on your computer if it is not running. If you need to capture the same trace again, you can directly start from step 3.

```cmd
logman delete msperf
```

## Uploading Captured Traces

If you are asked to upload the captured traces, please **Compress**/**zip** the entire folder (do not ignore this request) and upload the compressed file to the provided workspace.
