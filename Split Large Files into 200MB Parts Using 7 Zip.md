<br><table><td>WARNING</td><td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td></table><br>

Disclaimer: This content was generated with the assistance of AI and should be verified for accuracy and relevance to your specific use case.

## How to Split Large Files into 200MB Parts Using 7 Zip

When sharing large files it's often necessary to compress and split them into smaller chunks for easier distribution (e.g., via email, cloud storage, or USB). This guide walks you through how to use **7-Zip** to split a file or folder into multiple 200MB compressed parts.

### What You'll Need

- A file or folder you want to compress
- [7-Zip](https://www.7-zip.org/) installed on your Windows PC

### Step-by-Step Guide

#### Step 1: Locate the files or Folder

Use **File Explorer** to navigate to the files or folder you want to compress.

#### Step 2: Right-Click and Open 7-Zip

1. Right-click the files or a folder.
2. Hover over **7-Zip** in the context menu.
3. Select **"Add to archive..."**
(You may need to press and hold "Shift" then right click on the selected files/folder to be able to see 7-zip option)
![image](https://github.com/user-attachments/assets/09feeb61-d489-449e-8139-e9b9dbac57be)


#### Step 3: Configure Compression Settings

In the **Add to Archive** window, configure the settings as follows:
![image](https://github.com/user-attachments/assets/08ada49e-ff35-458b-b9f2-752301824b98)


> ✅ **Note**: Use **capital 'M'** for megabytes. Lowercase 'm' may be interpreted as megabits or result in errors.

#### Step 4: Start Compression

Click **OK** to begin the process. 7-Zip will create multiple files such as:

```

mydata.7z.001
mydata.7z.002
mydata.7z.003
...

```

Each part will be 200MB (except possibly the last one, which may be smaller).

---

### How to Extract the Split Archive

To ensure a smooth extraction experience for the recipient, provide them with the following simple instructions:

1. **Install [7-Zip](https://www.7-zip.org/)** if not already installed.
2. Place **all parts** (e.g., `.001`, `.002`, etc.) in the **same folder**.
3. Right-click the `.001` file.
4. Select **"7-Zip → Extract Here"** or **"Extract to folder\\…”**
5. 7-Zip will automatically combine all parts and extract the original file or folder.

> ⚠️ Ensure **none of the parts are missing or renamed**. All segments must be present for extraction to succeed.

---
