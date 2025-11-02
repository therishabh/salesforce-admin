# Salesforce Validation Rules Interview Master Guide

## 🧠 **Part 1: Core & Conceptual Questions (1 – 20)**

---

### **1. What is a Validation Rule in Salesforce?**

A **Validation Rule** is a formula expression that evaluates to `TRUE` or `FALSE` and prevents a record from being saved when the expression evaluates to `TRUE`.
It ensures that data entered into Salesforce meets specific business or data-quality standards.

**Example:**

```
ISBLANK(Email)
```

→ Displays an error message and stops the record from saving if `Email` is blank.

---

### **2. Purpose of a Validation Rule**

* Enforce **data integrity and business logic** at the platform level.
* Prevent **bad data** entry before records are committed to the database.
* Replace many simple Apex “before insert/update” validations.
* Maintain **consistent logic** across UI, API, and automation tools.

---

### **3. On Which Salesforce Objects Can Validation Rules Be Created?**

They can be created on:

* **Standard objects** (e.g., Account, Contact, Opportunity, Case)
* **Custom objects**
* **Custom metadata & settings:** No (but they can be referenced within formulas)
* **Activities (Task, Event):** Yes

---

### **4. How Does Salesforce Evaluate a Validation Rule?**

When a record is created or updated:

1. Salesforce calculates the formula.
2. If the formula returns `TRUE`, the system:

   * Displays the defined **error message**, and
   * **Rejects the DML operation** (record not saved).
3. If the formula returns `FALSE` or `NULL`, the record is saved.

---

### **5. What is the Return Type of a Validation Rule Formula?**

Always a **Boolean (TRUE/FALSE)**.
Only when the formula returns `TRUE` will it trigger the error message.

---

### **6. What Happens When a Validation Rule Evaluates to TRUE vs. FALSE?**

* `TRUE` → Error message is shown; record is **blocked from saving**.
* `FALSE` → Validation passes; record is **saved**.

---

### **7. Can You Create Multiple Validation Rules on a Single Object?**

✅ **Yes.**

* All active validation rules are evaluated when a record is saved.
* Salesforce displays the first 10 triggered error messages at once (per record).

**Best Practice:** Avoid overlapping rules; consolidate when possible.

---

### **8. Limitations of Validation Rules**

| Item                    | Limit                                |
| ----------------------- | ------------------------------------ |
| Max rules per object    | 500 active + inactive combined       |
| Formula size            | 3,900 characters                     |
| Compiled size           | 5,000 bytes                          |
| Error messages          | 255 characters                       |
| Cross-object references | Only **parent fields**, not children |

---

### **9. Difference Between Formula Fields and Validation Rules**

| Aspect          | Formula Field                   | Validation Rule                     |
| --------------- | ------------------------------- | ----------------------------------- |
| Purpose         | Calculates and displays data    | Enforces data quality before save   |
| Return type     | Can be text, number, date, etc. | Boolean only                        |
| Evaluation      | Every time the record is viewed | On record save (Insert/Update)      |
| Editable fields | None (read-only)                | Blocks edit/save if condition fails |

---

### **10. Can Validation Rules Reference Fields from Related Objects?**

Yes — but **only parent fields** (via lookup or master-detail).
Example:

```
ParentObject__r.Status__c = "Closed"
```

You cannot reference **child** records directly.

---

### **11. What Happens to Validation Rules During Data Import (Data Loader, API, Flow)?**

Validation rules are **enforced by default** for:

* UI entry
* API (including Data Loader)
* Flow updates

✅ They ensure data integrity across all entry points.
🚫 They cannot be bypassed automatically; you must build bypass logic.

---

### **12. How Can We Bypass Validation Rules During Data Migration or Automated Operations?**

Common methods:

1. **Checkbox Bypass Field** (e.g., `Bypass_Validation__c`) checked by automation users.
2. **$Profile.Name** or **$User.Role.Name** conditions in formula.
3. **Custom Permission** → more maintainable.
   Example:

   ```
   AND(
       NOT($Permission.Bypass_Validations),
       ISBLANK(Email)
   )
   ```
4. **Apex:** Temporarily deactivate or use “without sharing” context.

---

### **13. Can Validation Rules Be Conditional on Profile or User Role?**

Yes.
Use global variables:

```
$Profile.Name = "Standard User"
$UserRole.Name = "Sales Rep"
```

However, **best practice:** use **Custom Permission** instead of hardcoding names for scalability.

---

### **14. What’s the Execution Order of Validation Rules?**

**Key sequence in Salesforce transaction order:**

1. System validation (field format, required fields)
2. **Before Triggers**
3. **Custom Validation Rules**
4. Duplicate Rules
5. After Triggers
6. Assignment Rules → Workflow → Processes → Flows
7. Commit

So validation rules run **after before triggers** but **before workflows**.

---

### **15. Can You Use ISCHANGED, PRIORVALUE, and ISNEW in Validation Rules?**

✅ Yes. Examples:

* Prevent field update:

  ```
  AND(
      ISCHANGED(Status__c),
      PRIORVALUE(Status__c) = "Approved"
  )
  ```
* Detect new record:

  ```
  ISNEW()
  ```

---

### **16. Are Validation Rules Enforced When Using DML Operations in Apex?**

✅ Yes, unless:

* You use **Database.insert(record, false)** → partial success allows bypass of specific errors.
* You **deactivate** the rule temporarily.
  Otherwise, validation logic always fires, regardless of origin.

---

### **17. How Do You Handle Validation Errors in Apex Code?**

Use `try–catch` blocks or `Database.DMLResult`.

Example:

```apex
Database.SaveResult sr = Database.insert(acc, false);
if(!sr.isSuccess()) {
   for(Database.Error e : sr.getErrors()) {
      System.debug('Validation Failed: ' + e.getMessage());
   }
}
```

---

### **18. Can Validation Rules Reference Custom Settings or Custom Metadata?**

✅ Yes. Example:

```
AnnualRevenue > $CustomMetadata.Limits__mdt.Revenue_Limit__c
```

or

```
Amount > $Setup.GlobalLimits__c.Max_Amount__c
```

This is an excellent way to make rules **dynamic** and **configurable**.

---

### **19. Can You Use Validation Rules to Enforce Record-Level Security?**

🚫 No.
Validation Rules control **data integrity**, not **access**.
Use **OWD, Profiles, Permission Sets, and Sharing Rules** for record-level access control.

---

### **20. How Can You Debug or Test Validation Rules Effectively?**

* Use the **Formula Editor → Check Syntax**.
* Use **Developer Console → Save Logs** for Apex DMLs.
* In **Apex test classes**, simulate data to trigger both pass/fail paths.
* Temporarily display helper messages using **custom debug fields** or **error location "Top of Page"**.
* Use **Setup → Validation Rules → “Last Modified By”** to track which rule caused errors.

---

## 🧩 **Part 2: Scenario-Based Questions (21 – 32)**

**Focus:** Real-world business use cases and their formula-based solutions.

---

### **21. Conditional Enforcement**

**Scenario:** Prevent users from changing the “Close Date” after an Opportunity is **Closed Won**.

**Validation Rule Formula:**

```
AND(
   ISCHANGED(CloseDate),
   ISPICKVAL(StageName, "Closed Won")
)
```

**Explanation:**

* `ISCHANGED(CloseDate)` → detects any modification of Close Date.
* `ISPICKVAL(StageName, "Closed Won")` → fires only when Opportunity is already Closed Won.
* Together, they block edits to Close Date on finalized deals.

**Best Practice Tip:**
Use `PRIORVALUE(StageName)` if you only want to restrict changes after status transitions to Closed Won.

---

### **22. Field Dependency**

**Scenario:** “Reason for Loss” must be filled when Opportunity Stage = “Closed Lost”.

**Validation Rule Formula:**

```
AND(
   ISPICKVAL(StageName, "Closed Lost"),
   ISBLANK(Reason_for_Loss__c)
)
```

**Explanation:** Ensures users can’t mark deals as Closed Lost without explaining why.
**Error Message:** “Please specify the reason for loss before closing the opportunity.”

---

### **23. Date Validation**

**Scenario:** Prevent “Follow-up Date” from being in the past.

**Validation Rule Formula:**

```
Follow_Up_Date__c < TODAY()
```

**Explanation:** Simple yet common — stops users from scheduling follow-ups in the past.
**Error Message:** “Follow-up date cannot be earlier than today.”

---

### **24. Cross-field Logic**

**Scenario:** Ensure “End Date” is always later than “Start Date”.

**Validation Rule Formula:**

```
AND(
   NOT(ISBLANK(End_Date__c)),
   NOT(ISBLANK(Start_Date__c)),
   End_Date__c <= Start_Date__c
)
```

**Explanation:** Prevents illogical ranges like inverted date spans.

**Interview Tip:** Always wrap date comparisons with `ISBLANK` checks to avoid runtime formula errors.

---

### **25. Conditional Logic on Picklist**

**Scenario:** When `Type = "Customer"`, ensure “Account Number” is mandatory.

**Validation Rule Formula:**

```
AND(
   ISPICKVAL(Type, "Customer"),
   ISBLANK(AccountNumber)
)
```

**Error Message:** “Account Number is required for Customers.”

---

### **26. Profile-Based Rule**

**Scenario:** The rule should apply only for Standard Users, not Admins.

**Validation Rule Formula:**

```
AND(
   $Profile.Name <> "System Administrator",
   ISBLANK(Email)
)
```

**Best Practice:** Replace hardcoded profile names with **Custom Permission** for maintainability.

---

### **27. Bypass Logic with Custom Permission**

**Scenario:** Allow certain users (e.g., Integration User) to bypass all validations.

**Validation Rule Formula:**

```
AND(
   NOT($Permission.Bypass_Validation),
   ISBLANK(Important_Field__c)
)
```

**Explanation:**

* `$Permission.Bypass_Validation` → dynamic, tied to a Custom Permission.
* You can manage who gets that permission via Permission Sets.
  ✅ **Best, scalable way** to control bypass.

---

### **28. Data Migration Exception**

**Scenario:** While importing old data, you don’t want validations to fire, but want them active for UI users.

**Approach:**

1. Create a checkbox: `Bypass_Validation__c`.
2. Modify rule:

   ```
   AND(
       NOT(Bypass_Validation__c),
       ISBLANK(Critical_Field__c)
   )
   ```
3. In Data Loader, set that checkbox = TRUE for imported records.

**Alternative:** Use Custom Setting to control bypass org-wide.

---

### **29. Validation + Workflow Conflict**

**Scenario:** A workflow updates a field post-save that re-triggers a validation rule and causes recursion.

**Solution Approach:**

* Validation rules are triggered only **before save**, so if a workflow updates a field, it causes another save cycle.
* If that violates a validation rule → it fails.

**Fix:**

* Add condition to validation rule to **exclude workflow system context**, e.g.:

  ```
  AND(
      NOT($User.ProfileId = "Workflow Integration User"),
      <your existing condition>
  )
  ```
* Or restructure logic to avoid conflicting updates.

---

### **30. Before vs. After-Save Flow Interaction**

**Scenario:** A Before-Save Flow modifies a field that violates a validation rule.

**Explanation:**

* Validation rules fire **after before-save flows**.
* So, if the flow sets a value that triggers a validation rule → **the record fails to save**.

**Resolution Options:**

* Adjust flow logic to not produce invalid data.
* Add bypass logic in validation rule for system processes.
* Use `Custom Permission` check to exclude automation users.

---

### **31. Historical Data / Inactive Users**

**Scenario:** You need to edit legacy data that doesn’t comply with current rules.

**Solution:**

* Use a bypass field or custom permission.
* Temporarily deactivate rule during cleanup (only in sandbox/deployment window).
* Or wrap validation logic in a condition:

  ```
  AND(
      CreatedDate > DATE(2023,1,1),
      ISBLANK(New_Field__c)
  )
  ```

This ensures validation applies **only to records created after a certain date**.

---

### **32. Multi-Currency / Locale Issues**

**Scenario:** Ensure “Discount %” doesn’t exceed 20% for any currency and locale.

**Validation Rule Formula:**

```
Discount__c > 0.2
```

**Notes for global orgs:**

* Formula engine auto-handles currency conversions and locale decimal separators.
* Always store decimal thresholds (not currency fields) when comparing across regions.

**Best Practice:**
For currency-based validations, compare **same-currency fields**, or convert using parent currency field if needed.

---

## 🏗️ **Part 3: Advanced / Architectural Questions (33 – 42)**

---

### **33. How would you design validation logic that can be centrally managed and reused across multiple objects?**

**Problem:**
Organizations often repeat similar rules (e.g., email validation, date logic) across multiple objects — leading to duplication and maintenance issues.

**Approaches:**

1. **Custom Metadata or Custom Settings**

   * Store configurable values (e.g., “Minimum Age”, “Max Discount”) in metadata.
   * Reference them in formulas:

     ```
     Amount > $CustomMetadata.Limits__mdt.Max_Amount__c
     ```

2. **Reusable Formula Snippets (via Formula Field References)**

   * Create hidden formula fields that encapsulate logic (e.g., `Email_Is_Invalid__c`).
   * Reference them inside multiple validation rules.

3. **Dynamic Apex / Flows**

   * For highly dynamic use cases, manage rules in Apex (via validation frameworks) or as configurable flow decisions.

4. **Custom Permission Flags**

   * For toggling logic per user or process.

✅ **Best Practice:** Keep validation logic declarative when possible; move to metadata-driven Apex only when complexity or cross-object conditions exceed formula capabilities.

---

### **34. What are the pros and cons of implementing business logic in Validation Rules vs. Apex Triggers vs. Flows?**

| Aspect                  | Validation Rules      | Apex Triggers               | Flows                  |
| ----------------------- | --------------------- | --------------------------- | ---------------------- |
| **When it runs**        | Before save           | Before/After DML            | Before/After save      |
| **Best for**            | Data integrity checks | Complex logic, cross-object | Declarative automation |
| **Ease of maintenance** | High (UI-based)       | Medium–Low                  | High                   |
| **Error messaging**     | User-facing           | Must code                   | UI configurable        |
| **Reusability**         | Limited               | High                        | Moderate               |
| **Governance**          | Simple                | Needs framework             | Simple                 |

**Guideline:**

* Start with Validation Rules → move to Flow → finally Apex if logic needs cross-record DML or heavy computation.

---

### **35. How would you handle complex multi-object validations (e.g., ensure a child record’s value doesn’t exceed a parent’s limit)?**

**Validation Rules alone can’t check child records.**
To handle such cases:

**Options:**

1. **Apex Trigger (Before Insert/Update)**

   * Query parent record → compare → throw error via `addError()`.

   ```apex
   if(child.Amount__c > parent.Max_Limit__c) {
       child.addError('Amount exceeds parent limit.');
   }
   ```

2. **Before-Save Record-Triggered Flow**

   * Use a “Get Records” element to fetch parent → Decision → Update or stop.
   * Lightweight and declarative for single-record transactions.

3. **Roll-Up Summary Alternative**

   * Roll up child totals to parent and use validation on parent.

✅ **Best Practice:**
Use Validation Rules **only for single-record logic**.
Use Apex/Flow for **multi-record or cross-object validations**.

---

### **36. How do you version control validation rules in a CI/CD pipeline?**

**Methods:**

1. **Source-Driven Development (Git)**

   * Validation rules are stored in the object’s metadata XML (e.g., `objects/Account.object`).
   * Track changes in Git with commit messages.

2. **SFDX Source Format**

   * Each object’s metadata (fields, validation rules) is in modular, human-readable files.

3. **Deployment via Metadata API / Change Sets**

   * Validate and deploy through pipeline (Jenkins, GitHub Actions, Azure DevOps).

4. **Automated Tests**

   * Include Apex test classes to verify expected errors.

✅ **Best Practice:**
Use **scratch orgs** and **PR-based deployments** for validation rule lifecycle management.

---

### **37. How do you handle validation logic differences across environments (Sandbox vs Production)?**

**Problem:**
You may want stricter rules in production, relaxed ones in UAT or sandbox.

**Solutions:**

1. **Custom Setting or Custom Metadata Toggle:**

   ```
   AND(
      $CustomMetadata.EnvConfig__mdt.Enforce_Strict_Validation__c,
      ISBLANK(Critical_Field__c)
   )
   ```
2. **$Organization.Name or $User.Username Conditions:**
   Temporary, not recommended for long-term.

   ```
   AND(
      $Organization.Name = "Production Org",
      ISBLANK(Required_Field__c)
   )
   ```

✅ **Best Practice:**
Use **Custom Metadata** to centralize environment flags — easier to deploy and maintain.

---

### **38. How can Custom Metadata Types or Custom Settings make validation rules dynamic?**

**Use Case Example:**
You want to validate that `Amount` should not exceed a configurable maximum threshold.

**Custom Metadata Record:**

| Field         | Value         |
| ------------- | ------------- |
| Name          | Max_Threshold |
| Max_Amount__c | 10000         |

**Validation Rule:**

```
Amount > $CustomMetadata.Limits__mdt.Max_Amount__c
```

✅ **Advantage:**
Admins can update the threshold via Setup without editing the validation rule.

---

### **39. How to make a validation rule translatable or multi-lingual (for global orgs)?**

**Method 1: Use Translation Workbench**

* Create the rule with English error message.
* In **Setup → Translation Workbench → Override → Validation Rule**, translate error messages.

**Method 2: Custom Label**

* Reference in validation:

  ```
  ISBLANK(Email)
  ```

  with Error Message = `{!$Label.Email_Error_Message}`
* Translate the label in the Translation Workbench.

✅ **Best Practice:** Always use **Custom Labels** for global orgs.

---

### **40. What’s your approach when multiple teams maintain different validation rules that may overlap or conflict?**

**Governance Strategy:**

1. **Validation Rule Inventory:**
   Export all rules via Salesforce metadata → maintain in shared documentation.
2. **Ownership Assignment:**
   Assign rule owners or teams per object.
3. **Impact Analysis Before Activation:**
   Test new rules in UAT; check overlaps.
4. **Standard Naming Convention:**
   `VR_[Object]_[Purpose]_[Version]` (e.g., `VR_Opportunity_CloseDate_Lock_v2`)
5. **Testing Framework:**
   Maintain regression test suite to verify existing behavior after new rules.

✅ **Goal:** Central governance → prevent conflicting or redundant validations.

---

### **41. How do you ensure validation rules don’t break Apex test classes or automated integrations?**

**Typical Problems:**

* Validation rules block DML in existing test data.
* Integration users hit unexpected validation errors.

**Mitigation:**

1. **Use Custom Permissions / Bypass Field**

   ```
   AND(
       NOT($Permission.Bypass_Validation),
       ISBLANK(Required_Field__c)
   )
   ```
2. **Include Valid Data in Tests**
   Update test data factory classes to comply with active rules.
3. **Test Automation User Context**
   Add bypass permission set for automated users.

✅ **Best Practice:**
Treat validation rules as part of your “data contract” — test them alongside Apex.

---

### **42. How can Custom Permissions be used for conditional validation enforcement?**

**Best-Practice Approach for Large Orgs**

**Step 1:**
Create a **Custom Permission** named `Bypass_Validation`.

**Step 2:**
Add to Permission Sets (e.g., “Integration User Permissions”).

**Step 3:**
Reference in formula:

```
AND(
   NOT($Permission.Bypass_Validation),
   ISBLANK(Critical_Field__c)
)
```

✅ **Advantages:**

* Fully declarative, no profile hardcoding.
* Dynamic control without changing metadata.
* CI/CD friendly (Custom Permissions deploy easily).

---

## ⚙️ **Part 4: Hands-On / Practical Questions (43 – 52)**
This section focuses on **formula writing, real-time use cases, Apex testing, and debugging**, exactly what senior-level technical interviews or live coding rounds include.

---

### **43. Write a validation rule that prevents negative values in the “Amount” field**

**Formula:**

```
Amount < 0
```

**Explanation:**
Blocks records where Amount is negative.
**Error Message:** “Amount cannot be negative.”
**Best Practice:** Always test with blank fields to ensure no unintended firing; wrap with `NOT(ISBLANK(Amount))` if needed.

---

### **44. Write a validation rule to ensure that Email field contains “@” and “.”**

**Formula:**

```
AND(
   NOT(CONTAINS(Email, "@")),
   NOT(CONTAINS(Email, "."))
)
```

**Explanation:**

* Ensures a very basic email structure.
* For stricter pattern matching, Salesforce doesn’t allow full regex, so use a combination of functions.

**Alternative:** Use standard email field type → automatically validated.

---

### **45. Write a validation rule to prevent updates once record is approved (Approval_Status = "Approved")**

**Formula:**

```
AND(
   ISPICKVAL(Approval_Status__c, "Approved"),
   NOT(ISNEW())
)
```

**Explanation:**

* Allows creation but blocks edits if record is already approved.
* Common in controlled processes (e.g., quotes, pricing, or legal docs).

---

### **46. Write a validation rule to ensure “Annual Revenue” is entered only if Type = “Customer”**

**Formula:**

```
AND(
   NOT(ISPICKVAL(Type, "Customer")),
   NOT(ISBLANK(AnnualRevenue))
)
```

**Explanation:**
Prevents filling unnecessary data for non-customer accounts.
**Error Message:** “Annual Revenue should only be entered for Customer accounts.”

---

### **47. Write a validation rule to ensure “Discount Percentage” cannot exceed 20% for non-admins**

**Formula:**

```
AND(
   $Profile.Name <> "System Administrator",
   Discount_Percentage__c > 0.2
)
```

**Best Practice:**
Replace `$Profile.Name` with a custom permission:

```
AND(
   NOT($Permission.Allow_High_Discount),
   Discount_Percentage__c > 0.2
)
```

This keeps logic clean and avoids profile hardcoding.

---

### **48. What happens if a validation rule formula includes a null field reference?**

**Behavior:**

* Salesforce treats **null as 0 or blank**, depending on the field type.
* Example:

  ```
  Amount__c > Discount__c
  ```

  → If `Discount__c` is blank, it is treated as 0.
* To avoid null issues, wrap with `ISBLANK()` or `NOT(ISBLANK())`.

✅ **Tip:** Always check for blank fields explicitly to avoid false positives.

---

### **49. Demonstrate how to unit test a validation rule in an Apex test class**

**Example Apex:**

```apex
@IsTest
private class AccountValidationTest {
    @IsTest
    static void testAccountWithoutEmail() {
        Account acc = new Account(Name = 'Test Account');
        Test.startTest();
        try {
            insert acc;
            System.assert(false, 'Expected validation error');
        } catch (DmlException e) {
            System.assert(e.getMessage().contains('Email is required'));
        }
        Test.stopTest();
    }
}
```

**Key Points:**

* Test both pass and fail scenarios.
* Ensure meaningful error message is asserted.
* Never disable validation rules in tests.

---

### **50. How do you disable a validation rule temporarily in sandbox without deleting it?**

**Options:**

1. **Uncheck “Active” checkbox** — simplest and recommended for temporary disable.
2. **Wrap logic inside a bypass condition:**

   ```
   AND(
       NOT($Setup.GlobalConfig__c.Disable_Validations__c),
       <your existing formula>
   )
   ```
3. **Comment Out Formula:** Temporarily comment with `/* … */` during testing.

✅ Always re-enable and regression test before deploying to production.

---

### **51. How would you track changes to validation rules across deployments (Metadata API / Git)?**

**Answer:**

* Validation Rules are stored in metadata XML under:
  `/objects/ObjectName.object`
* Each `<validationRules>` tag defines name, error condition formula, and message.
* Use **SFDX + Git** to:

  * Commit each metadata change.
  * Compare via diffs in pull requests.
  * Include change review (especially for production-impact rules).

✅ **Tip:** Treat validation rule changes like code — require PR reviews and QA validation.

---

### **52. How can you make a validation rule dependent on a toggle (checkbox field)?**

**Use Case:**
Admins want to disable a specific validation rule without deactivation.

**Formula:**

```
AND(
   NOT(Bypass_Validation__c),
   ISBLANK(Critical_Field__c)
)
```

**Explanation:**

* When `Bypass_Validation__c = TRUE`, rule will not fire.
* Useful for maintenance windows or specific data imports.

✅ **Best Practice:**
Mark bypass fields **hidden from end users** (use field-level security).

---

## 🧩 **Part 5: Trick & Edge-Case Questions (53–62)**
Part 5 focuses on **Trick & Edge-Case Questions (53–62)** — the hidden behaviors, platform limits, and less-documented rules that differentiate an *experienced developer* from a *formula-level admin*.

---

### **53. What happens if a validation rule formula references a field that no longer exists?**

**Behavior:**

* The validation rule becomes **invalid** and **cannot be saved or deployed**.
* Any existing references show as **“Field does not exist”** error in Setup.
* If you delete a field **used by an active validation rule**, Salesforce will automatically **deactivate** the rule.

**Best Practice:**
Use **Setup → Where is this used?** before deleting any field to avoid hidden dependencies.

---

### **54. What’s the maximum formula size allowed for a validation rule?**

| Type                 | Limit            |
| -------------------- | ---------------- |
| Formula characters   | 3,900 characters |
| Compiled size        | 5,000 bytes      |
| Error message length | 255 characters   |

**Notes:**

* Compiled size is what Salesforce evaluates internally after parsing.
* You can’t see compiled size directly, but long nested formulas are common culprits.
* Simplify logic using helper fields or smaller reusable formulas.

---

### **55. What happens if two validation rules return TRUE at the same time?**

**Behavior:**

* Salesforce displays **up to 10 error messages per record** simultaneously.
* Each error message appears in its defined **location** (field-level or top of page).
* No guaranteed order of execution or display — they’re evaluated independently.

**Best Practice:**

* Avoid overlapping logic (e.g., two rules checking same field).
* Combine related logic into a single rule for better UX.

---

### **56. How do validation rules behave when triggered from Process Builder or Flow updates?**

**Answer:**

* Any DML operation — including from **Process Builder** or **Flow** — triggers **validation rules again**.
* Validation Rules are **not skipped** for automation updates unless you explicitly design bypass conditions.

**Solution Example:**
Add a bypass condition:

```
AND(
   NOT($User.Profile.Name = "Automation User"),
   ISBLANK(Critical_Field__c)
)
```

✅ **Best Practice:**
Use a dedicated **“System Automation” user** or **custom permission flag** for Flows to prevent infinite save failures.

---

### **57. Can you create a validation rule that references a formula field?**

✅ **Yes.**

Example:

```
AND(
   Formula_Field__c > 0,
   ISBLANK(Another_Field__c)
)
```

**Caveat:**
If the **formula field depends on other fields**, and they are updated in the same transaction, the validation rule evaluates using the **newest runtime values** (not old ones).

**Best Practice:** Keep formula logic simple and avoid circular dependencies.

---

### **58. Can you deploy validation rules via Change Set or Metadata API?**

✅ **Yes.**
Validation Rules are part of object metadata.

**Deployment Options:**

1. **Change Sets** → Add Object → Include Validation Rules.
2. **SFDX / Metadata API** → Deploy `/objects/ObjectName.object` XML.
3. **Ant Migration Tool / CI/CD Pipelines** → Recommended for automated deployment.

**Tip:**
Validation rules are **activated by default** on deployment unless set to false in metadata XML.

---

### **59. How do you localize validation rule error messages for multi-language orgs?**

**Two Methods:**

1. **Translation Workbench:**

   * Go to Setup → Translation Workbench → Override → Validation Rule Messages.
   * Add translations per active language.

2. **Custom Labels:**

   * Reference in rule as:
     `Error Message = {!$Label.Validation_Error_Msg}`
   * Translate labels via Translation Workbench.

✅ **Best Practice:**
Use **Custom Labels** if your org supports frequent translation updates or dynamic languages.

---

### **60. What happens if a validation rule’s error field is deleted?**

**Behavior:**

* The rule **remains active**, but the **error message moves to the top of the page**.
* The rule doesn’t break; it just loses its field-level anchor.

**Fix:**
Edit the rule → choose a valid field again in “Error Location.”

---

### **61. Does `System.runAs()` in Apex bypass validation rules?**

🚫 **No.**
`System.runAs()` changes the **user context**, not the system execution level.

Validation rules still run and can fail even under `runAs()`.
To bypass them, use:

* Custom Permission-based bypass logic, or
* Deactivate the rule temporarily.

---

### **62. What’s the difference between “Error Location: Field” vs “Top of Page”?**

| Option          | Behavior                                                                                                       |
| --------------- | -------------------------------------------------------------------------------------------------------------- |
| **Field**       | Displays the error next to a specific field. Improves UX.                                                      |
| **Top of Page** | Shows a red message banner at top of the record page. Used for record-level errors or cross-field validations. |

**Best Practice:**

* Use **Field location** when error is tied to one field.
* Use **Top of Page** for combined or record-level logic (e.g., Start/End Date inconsistencies).

---

## 📘 **Part 6: Validation Rules Complete Summary + Study Sheet – Senior Developer Study Sheet**

---

### 🧠 **Core Concepts**

| # | Question                                          | Short Answer                                                                                   |
| - | ------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| 1 | What is a validation rule?                        | A formula that returns TRUE to prevent record save. Enforces business logic at the data layer. |
| 2 | When do validation rules execute?                 | After “before triggers” and before “after triggers.”                                           |
| 3 | What is the syntax for a validation rule formula? | Logical formula returning TRUE/FALSE; TRUE blocks save.                                        |
| 4 | Can you reference related object fields?          | Yes, using cross-object formulas on master-detail lookups.                                     |
| 5 | Can validation rules be bypassed by API or Apex?  | No, unless explicitly bypassed using formula logic or custom permissions.                      |
| 6 | How are they deployed?                            | Through Change Sets or Metadata API as part of object metadata.                                |
| 7 | What’s the purpose of error location?             | To specify where the message appears (field or top of page).                                   |

---

### ⚙️ **Common Scenarios**

| # | Use Case                                    | Formula Example                                                   |
| - | ------------------------------------------- | ----------------------------------------------------------------- |
| 1 | Prevent blank email                         | `ISBLANK(Email)`                                                  |
| 2 | Restrict future Close Date                  | `CloseDate > TODAY()`                                             |
| 3 | Prevent changing Opportunity Stage backward | `ISPICKVAL(PRIORVALUE(StageName), "Closed Won")`                  |
| 4 | Ensure phone format                         | `NOT(REGEX(Phone, "\\d{3}-\\d{3}-\\d{4}"))`                       |
| 5 | Prevent modification after approval         | `AND(ISPICKVAL(Status, "Approved"), NOT(ISNEW()))`                |
| 6 | Restrict discount to ≤20%                   | `AND($Profile.Name <> "System Administrator", Discount__c > 0.2)` |
| 7 | Make field mandatory based on another       | `AND(ISPICKVAL(Type, "Customer"), ISBLANK(AnnualRevenue))`        |

---

### 🧩 **Advanced Techniques**

| # | Topic                           | Key Insight                                                                       |
| - | ------------------------------- | --------------------------------------------------------------------------------- |
| 1 | **Bypass Flags**                | Add checkbox field like `Bypass_Validation__c` or `$Permission.Skip_Validations`. |
| 2 | **System Automation Exemption** | Exclude Flows/Processes by checking `$User.Profile.Name`.                         |
| 3 | **Custom Labels for i18n**      | Use `$Label.Validation_Error` for translated error messages.                      |
| 4 | **Testing in Apex**             | Assert `DmlException` messages to validate rules trigger correctly.               |
| 5 | **Version Control**             | Validation rules stored in `<validationRules>` XML under object metadata.         |

---

### ⚡ **Edge Cases & Tricky Behaviors**

| # | Edge Case                 | Behavior / Tip                                |
| - | ------------------------- | --------------------------------------------- |
| 1 | Field deleted from rule   | Rule is deactivated automatically.            |
| 2 | Two rules true at once    | Both show messages; max 10 at a time.         |
| 3 | Formula field referenced  | Evaluates using latest transaction value.     |
| 4 | Null value handling       | Treated as 0 or blank; wrap with `ISBLANK()`. |
| 5 | Flow update triggers rule | Yes, all DML triggers validation rules.       |
| 6 | `System.runAs()` bypass   | No, it only changes user context.             |
| 7 | Error field deleted       | Error moves to “Top of Page.”                 |

---

### 🧪 **Testing Checklist (For Apex or QA)**

✅ Insert record → Should fail for invalid data
✅ Update existing → Should fire when rule condition met
✅ Bulk Insert / Data Load → Confirm behavior
✅ System User / Integration → Verify bypass logic
✅ Deactivate & Reactivate → Confirm regression passes

---

### 💡 **Best Practices Summary**

| Area                | Practice                                          |
| ------------------- | ------------------------------------------------- |
| **Design**          | One rule per logical condition – avoid overlap    |
| **Performance**     | Keep formula <3,900 chars; break complex logic    |
| **Maintainability** | Use custom permissions instead of `$Profile.Name` |
| **Error UX**        | Write clear, specific messages                    |
| **Deployment**      | Include rules in CI/CD; track via Git diffs       |
| **Testing**         | Cover both pass & fail in unit tests              |
| **Translation**     | Use custom labels for error messages              |

---

### 🧮 **Formula Reuse Snippets**

```
/* Prevent Record Edit after Approval */
AND(
   ISPICKVAL(Status__c, "Approved"),
   NOT(ISNEW())
)

/* Require Close Date <= Today */
CloseDate > TODAY()

/* Allow Admin Override */
AND(
   NOT($Permission.Allow_Override),
   <main_condition_here>
)
```

---

### 🧭 **Final Takeaway for Senior Developers**

* Validation rules are **data-level enforcement**, not UI-level.
* They impact **all DML contexts**, so always plan **bypass and automation compatibility**.
* For enterprise-grade orgs, manage them like code:
  ➤ Version control,
  ➤ Automated deployment,
  ➤ Apex coverage,
  ➤ Documentation.

---
