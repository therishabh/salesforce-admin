# 🧩 Salesforce Field Dependency — Complete Interview Q&A (Senior Developer Level)

---

## 1️⃣ What is Field Dependency in Salesforce?

**Answer:**
Field Dependency allows you to **filter the available values of one picklist (Dependent Field)** based on the **selected value of another picklist or checkbox (Controlling Field)**.
It helps create dynamic, context-sensitive picklist behavior in forms, reducing user errors and ensuring data consistency.

**Example:**
If *Country = India*, then only *Indian States* appear in the State picklist.

---

## 2️⃣ What are the two types of fields in a field dependency?

* **Controlling Field:** Determines which dependent field values are available.
* **Dependent Field:** Displays values filtered by the controlling field.

---

## 3️⃣ Which field types support field dependency?

| Field Type            | Controlling | Dependent |
| --------------------- | ----------- | --------- |
| Picklist              | ✅           | ✅         |
| Multi-Select Picklist | ❌           | ✅         |
| Checkbox              | ✅           | ❌         |

---

## 4️⃣ Can a Text, Number, or Formula field be used in field dependency?

**Answer:**
No. Field Dependency only works with **Picklist**, **Multi-Select Picklist**, and **Checkbox** fields.
Formula or Text fields cannot control picklist behavior directly.

---

## 5️⃣ Can you create multi-level dependencies (e.g., Country → State → City)?

**Answer:**
Yes. Salesforce supports **multi-level dependencies**, where:

* Country → controls → State
* State → controls → City
  Each level must respect the field type and limit constraints.

---

## 6️⃣ What are the maximum limits for controlling and dependent fields?

| Field Type           | Max Values | Notes                                     |
| -------------------- | ---------- | ----------------------------------------- |
| Controlling Picklist | 300        | Includes inactive values                  |
| Dependent Picklist   | 1000       | Can depend on multiple controlling values |

---

## 7️⃣ What happens when a controlling or dependent field is deleted and undeleted?

**Answer:**
If either field is deleted and then undeleted, **the dependency mapping is lost**.
You must **recreate** the field dependency manually.

---

## 8️⃣ Can we hide/show fields using field dependency?

**Answer:**
❌ No. You can only hide/show **values** inside picklists, not the fields themselves.
For field visibility, use **Dynamic Forms**, **Record Types**, or **Page Layouts**.

---

## 9️⃣ What is the character limit for picklist values?

* Each picklist value: **255 characters** max.
* Total character limit per picklist: **15,000 characters** (sum of all values).
  If exceeded, Salesforce throws an error.

---

## 🔟 What is “LOV” in the context of Field Dependency?

**Answer:**
LOV = **List of Values** — all the options displayed in a picklist dropdown.
You can bulk-add LOVs via **copy-paste from Excel**, or automate using **Metadata API**.

---

## 11️⃣ What are the limitations of field dependency?

1. Only works for Picklist, Multi-select Picklist, and Checkbox fields.
2. Must be configured manually — not ideal for large datasets.
3. Dependencies are **lost on undelete**.
4. Only controls values, **not field visibility**.
5. No dependency across **different objects**.
6. Not supported for **standard picklists** like Stage, Lead Status, etc. (unless custom).

---

## 12️⃣ What’s the error — “The field you chose is directly or indirectly dependent on itself”?

**Answer:**
Occurs when a field is mistakenly set as both **controlling** and **dependent** (directly or indirectly).
**Fix:** Remove circular dependency and verify hierarchy.

---

## 13️⃣ If a standalone picklist has 1200 values, what could be the issue?

**Answer:**
It exceeds the **maximum limit of 1000 values** or the **total 15,000 character limit**.
Solution:

* Reduce picklist values
* Split into dependent picklists
* Use custom objects for data-driven picklists

---

## 14️⃣ What’s the difference between field dependency and record type–based picklist values?

| Aspect          | Field Dependency | Record Type                 |
| --------------- | ---------------- | --------------------------- |
| Control Level   | Between fields   | Between record types        |
| Purpose         | Dynamic UI       | Business process separation |
| Dependency Type | Field-to-field   | Record type–to-field        |

---

## 15️⃣ Can a dependent field also be a controlling field?

**Answer:**
✅ Yes, this is allowed for **multi-level dependencies**, e.g.:
Country (C) → State (D + C) → City (D).

---

## 16️⃣ Can one controlling field control multiple dependent fields?

**Answer:**
✅ Yes, a single controlling field can control **multiple dependent fields**.

---

## 17️⃣ Can we use field dependency between fields from different objects?

**Answer:**
❌ No. Field dependencies only work **within the same object**.

---

## 18️⃣ How can we deploy field dependencies from sandbox to production?

**Answer:**
Include both fields and their **FieldDependency metadata** in the Change Set, or use the **Metadata API / ANT tool**.
If dependency isn’t deployed, dependent values won’t appear correctly.

---

## 19️⃣ Can we create or modify field dependencies using Apex?

**Answer:**
❌ No, Apex cannot modify metadata like field dependencies.
Use **Metadata API** for programmatic control.

---

## 20️⃣ Can we simulate dependency-like behavior for other field types (e.g., Lookup or Text)?

**Answer:**
Yes — using **Lightning Components (LWC)**, **Flows**, or **Screen Flows** with conditional visibility.

---

## 21️⃣ How to handle large dependencies (1000+ values) efficiently?

**Answer:**

* Use **Custom Objects + Lookup Fields** to store values dynamically.
* Use **LWC picklist filtering** for large datasets.
* Avoid massive static picklists.

---

## 22️⃣ How do dependencies behave in APIs (Data Loader, Integration, etc.)?

**Answer:**
Dependencies are **not enforced at API level** — you can insert values that violate dependency rules.

---

## 23️⃣ What’s the best way to export or view existing field dependencies?

**Answer:**
Use **Workbench** or **Metadata API** to fetch the `FieldDependencies` metadata definition.

---

## 24️⃣ Can we have field dependencies on Global Picklists?

**Answer:**
✅ Yes, but both fields must use the **same Global Picklist Value Set**.

---

## 25️⃣ What happens if we use Translation Workbench with field dependencies?

**Answer:**
Translations must exist for **both controlling and dependent field values**, or dependency mapping may break for localized users.

---

## 26️⃣ Can we create dependencies on Standard Picklists?

**Answer:**
Partially — some standard picklists (like *Stage*, *Lead Source*) don’t support it.
You can create **custom picklists** to replicate that functionality.

---

## 27️⃣ Can we restrict dependent field values for inactive controlling values?

**Answer:**
Yes, but only manually — Salesforce does not automatically remove dependencies tied to inactive controlling values.

---

## 28️⃣ How do dependencies behave in Lightning vs Classic?

**Answer:**
Behavior is identical; dependency logic is stored at the **metadata level**, not UI.

---

## 29️⃣ How do you document field dependencies for large projects?

**Answer:**
Use **Schema Builder** or **Workbench Metadata Export** to extract and map dependencies into Excel for documentation.

---

## 30️⃣ Can you migrate only dependency mapping (without field definitions)?

**Answer:**
No. Both fields must exist in target org before dependency mapping can be deployed.

---

## 31️⃣ How do you troubleshoot a missing dependent field value?

**Answer:**

1. Verify dependency mapping setup.
2. Check controlling field value.
3. Check record type value restrictions.
4. Check user’s profile field-level security.

---

## 32️⃣ Can you dynamically show/hide dependent values on LWC or Flow screens?

**Answer:**
Yes — use **Dynamic Picklist in LWC** or **Record Choice Sets in Flow** based on selected value.

---

## 33️⃣ Are dependencies case-sensitive?

**Answer:**
No — Salesforce treats picklist values as **case-insensitive** for dependency matching.

---

## 34️⃣ How does dependency behave in Dynamic Forms?

**Answer:**
Dynamic Forms control **field visibility**, while field dependencies control **value availability**. Both can coexist.

---

## 35️⃣ Can you have dependencies in managed packages?

**Answer:**
Yes, but they must be defined within the package.
Dependencies cannot reference fields from outside the managed package.

---

## 36️⃣ What is the storage format of field dependencies in metadata?

**Answer:**
They’re stored under `<fieldDependencies>` in the object’s `.object` XML file, defining `<controllingField>` and `<dependentField>` mappings.

---

## 37️⃣ How do dependencies interact with formula default values?

**Answer:**
Formula default values are **not influenced** by dependencies — dependency logic only applies to UI picklist value rendering.

---

## 38️⃣ Can you control dependent field values based on multiple controlling fields?

**Answer:**
Yes — one dependent field can depend on up to **10 controlling fields** (Salesforce limit).

---

## 39️⃣ Can dependencies affect validation rules or workflows?

**Answer:**
Indirectly — since invalid combinations might be prevented by dependency, fewer workflow triggers or validation errors occur.

---

## 40️⃣ What’s the difference between Field Dependency and Dynamic Picklist via Metadata API?

| Aspect           | Field Dependency   | Dynamic Picklist        |
| ---------------- | ------------------ | ----------------------- |
| Configuration    | UI-based setup     | Code or Metadata-based  |
| Supported Fields | Picklist, Checkbox | Any field type          |
| Runtime Behavior | Static (metadata)  | Dynamic (runtime logic) |

---

# 🧠 Bonus — Senior-Level Tricky Questions

41. **How would you handle a picklist dependency requirement where values change based on both Region and Product Type?**
    → Create **two controlling fields** and map both to the dependent field (multi-controlling dependency).

42. **If you deploy a field dependency to Production but dependent values don’t show, what do you check first?**
    → Ensure both fields and their values exist in target org and are included in metadata deployment.

43. **What’s the most efficient way to replicate field dependency behavior for 50+ combinations across objects?**
    → Use **Custom Metadata Types or Custom Settings** to store mappings, and reference via **Apex or LWC**.

44. **How do you handle performance when picklist dependencies are huge (e.g., 1000x300 matrix)?**
    → Consider **dynamic UI rendering** in LWC or breaking data into smaller logical groups.

45. **How to handle dependencies in a multilingual org with 5+ language translations?**
    → Maintain translation sets for both controlling and dependent values and validate mapping consistency per locale.
