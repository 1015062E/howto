<br><table><td>WARNING</td><td>Please refer to this document with an understanding of the potential risks involved. Proceed at your own discretion.</td></table><br>

**Disclaimer:** This content was generated with the assistance of AI and should be verified for accuracy and relevance to your specific use case.

## Troubleshooting Power BI Desktop Memory Errors During Data Refresh

When working with large datasets or complex transformations in Power BI Desktop, you may encounter the following error message during a data refresh:

> **"Failed to save modifications to the server. Error returned: 'There's not enough memory to complete this operation. Please try again later when there may be more memory available.'"**

This error typically indicates that **Power BI Desktop has exhausted the available memory (RAM)** on the local machine. Below are structured steps and tips to help you identify the cause and resolve the issue effectively.

---

### 🧭 Initial Troubleshooting Recommendations

Before diving into advanced configuration, try these basic steps:

- ✅ Use the **64-bit** version of Power BI Desktop (not 32-bit).
- ✅ Close other memory-intensive applications while refreshing.
- ✅ Apply filters in Power Query to reduce the data volume.
- ✅ Simplify complex **transformations**, **joins**, and **calculated columns**.
- ✅ Consider increasing your system’s **RAM** if feasible.

For detailed optimization guidance:
- [Optimize a model for performance in Power BI – Microsoft Learn](https://learn.microsoft.com/en-us/training/modules/optimize-model-power-bi/)
- [Optimization guide for Power BI](https://learn.microsoft.com/en-us/power-bi/guidance/power-bi-optimization)

---

### 🔍 Step-by-Step Diagnosis: Individual vs. Full Refresh

#### ✅ Test: Refresh a Single Table
Try refreshing one table individually by right-clicking on it and selecting **Refresh Data**. If this works but full refresh still fails:

---

### ⚙️ Step 1: Control Maximum Concurrent Jobs (Per PBIX File)

Power BI may attempt to refresh multiple tables in parallel, which can exceed available memory. You can limit this behavior:

**How to configure:**
1. Go to `File` → `Options and settings` → `Options`
2. Under **Current File** → `Data Load`
3. Adjust the setting under **Parallel loading of tables**:
   - **One** – to refresh tables sequentially, reducing memory pressure
   - **Custom** – define a number between 1–30 based on model size and refresh performance

> **Note:** Power BI Pro capacity limits may override values higher than 6.

---

### ⚙️ Step 2: Adjust Power Query Evaluation Settings (Global)

These settings control how many Power Query evaluations run in parallel and how much memory each one can use.

**Steps:**
1. Go to `File` → `Options and settings` → `Options`
2. Under **Global** → `Data Load`
3. Modify the following values:
   - **Maximum number of simultaneous evaluations**
   - **Maximum memory used per simultaneous evaluation (MB)**

🔽 **Recommendation:** Decrease these values if experiencing memory issues, especially on devices with limited hardware.

> **Important:** You must **restart Power BI Desktop** for these changes to take effect.

More details:
- [Evaluation configuration settings for Desktop – Power BI | Microsoft Learn](https://learn.microsoft.com/en-us/power-bi/create-reports/desktop-evaluation-configuration)

---

### 🚨 If Individual Table Refresh Still Fails

If refreshing a single table also fails with the same error, this likely means:
- The **model or transformation** is too large/complex for available memory.
- Even **one evaluation** exceeds the memory budget.

#### 🔧 At this point, optimize the report further:
- Simplify Power Query steps
- Remove unnecessary calculated tables/columns
- Split large reports into multiple PBIX files
- Use **DirectQuery** where appropriate

---

### ✅ Summary

| Scenario                                   | Suggested Action                                                                 |
|-------------------------------------------|----------------------------------------------------------------------------------|
| Single table refresh works, full fails    | Reduce **max concurrent jobs** / tweak **evaluation settings**                  |
| Single table refresh also fails           | **Revise report model** and **optimize query logic**                            |
| Using limited hardware                    | Reduce memory/evaluation settings, avoid large in-memory joins                  |
| Need better performance with large models | Consider splitting model or using DirectQuery                                   |

---

This guidance is designed to help you better manage memory consumption during Power BI Desktop refreshes. If you continue facing issues after trying the above configurations, further profiling and model tuning may be necessary.

---
