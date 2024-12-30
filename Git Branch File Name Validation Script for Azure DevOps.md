## Git Branch File Name Validation Script for Azure DevOps

<br><table><td>WARNING</td><td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td></table><br>

### Overview

In this post, we'll discuss how to create a PowerShell script for validating file names in a Git branch within an Azure DevOps repository. The script checks for forbidden characters, leading/trailing spaces, and long file paths, ensuring compliance with Azure DevOps file naming restrictions.

### Prerequisites

Before proceeding with the script, ensure that you:
- Have a local Git repository set up for your Azure DevOps project.
- Have PowerShell installed on your system.
- Are familiar with basic Git and Azure DevOps concepts.

### Azure DevOps Naming Restrictions

Azure DevOps has specific limitations when it comes to branch and file names, such as:
- **Forbidden characters** in file or folder names (e.g., `*`, `?`, `|`, etc.).
- **File path length** exceeding 250 characters.
- **Leading or trailing spaces** or dots in file names.
- The maximum **branch name length** is 244 characters.

Violating these constraints may result in errors when pushing changes or syncing files, so it’s crucial to ensure your branch and file names are compliant.

### The Script: PowerShell for Validation

Below is the PowerShell script that checks for the following file naming issues:
- Forbidden characters.
- Leading/trailing spaces or dots.
- File paths that exceed 250 characters.

```powershell
# Define the branch name
$branch = "your-branch-name-here"  # Replace with your branch name

# Check if inside a Git repository
if (-not (git rev-parse --is-inside-work-tree)) {
    Write-Host "Error: This script must be run from within a Git repository." -ForegroundColor Red
    exit
}

# Switch to the branch
Write-Host "Switching to branch $branch"
git checkout $branch | Out-Null

# Forbidden characters to check
$forbiddenChars = @('>', '<', ':', '"', '\', '|', '*', '?')

# Check for forbidden characters in file names (excluding files starting with '.' or ending in .png)
Write-Host "Checking for forbidden characters..."
$files = git ls-tree -r $branch --name-only
foreach ($file in $files) {
    # Skip files starting with a dot or ending with .png
    if ($file -match '^\.' -or $file -match '\.png$') {
        continue
    }

    # Split the file path into parts by '/'
    $fileParts = $file -split '/'
    
    # Check each part of the file path
    foreach ($part in $fileParts) {
        foreach ($char in $forbiddenChars) {
            if ($part.Contains($char)) {
                Write-Host "Forbidden character '$char' found in: $file" -ForegroundColor Yellow
            }
        }
    }
}

# Check for leading/trailing spaces or dots in file names (skip files starting with a dot)
Write-Host "Checking for leading/trailing spaces or dots..."
foreach ($file in $files) {
    if ($file -match '^\.' -or $file -match '\.png$') {
        continue
    }

    if ($file -match '^[\s.]|[\s.]$') {
        Write-Host "Leading or trailing space/dot found in: $file" -ForegroundColor Yellow
    }
}

# Check for file path lengths > 250 characters
Write-Host "Checking for file path lengths > 250..."
foreach ($file in $files) {
    if ($file -match '^\.' -or $file -match '\.png$') {
        continue
    }

    if ($file.Length -gt 250) {
        Write-Host "File path exceeds 250 characters: $file" -ForegroundColor Yellow
    }
}

Write-Host "Checks completed." -ForegroundColor Green
```

### Steps to Clone and Setup

Before running the script, you'll need to clone your repository and check out the correct branch:

1. Clone the repository (replace `your-repository-url-here` with your actual repository URL):
   ```bash
   git clone https://dev.azure.com/your-organization-name/_git/your-repository-name
   cd your-repository-name
   ```

2. Checkout the desired branch (replace `your-branch-name-here` with the branch you want to check):
   ```bash
   git checkout your-branch-name-here
   ```

### How It Works

The script performs the following tasks:
1. **Forbidden Characters**: Checks for characters like `*`, `?`, `|`, etc., in the file names.
2. **Leading/Trailing Spaces or Dots**: Flags file names that start or end with a space or dot.
3. **File Path Length**: Flags file paths that exceed 250 characters.

Additionally, the script skips files starting with a dot (`.`) or having `.png` extensions, which are often system files or media files that don't need to be validated in this context.

### Running the Script

1. Save the script as `check_branch.ps1` in your local repository directory.
2. Open **PowerShell** and navigate to your Git repository:
   ```powershell
   cd C:\path\to\your\repository
   ```
3. Run the script:
   ```powershell
   .\check_branch.ps1
   ```

### Ref: 
<br>https://learn.microsoft.com/en-us/fabric/cicd/git-integration/intro-to-git-integration?tabs=azure-devops#directory-name-limitations

### Benefits

By using this script, you can easily ensure that your file names comply with Azure DevOps' restrictions, avoiding issues when committing or pushing changes. It automates the process, reducing the manual effort involved in checking file names before pushing to the repository.

---

### Disclaimer

This content was generated with the assistance of AI and should be verified for accuracy and relevance to your specific use case.
