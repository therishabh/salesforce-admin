# 🚀 **Salesforce Page Layout **

---

# **1️⃣ Page Layout vs Lightning Record Page me kya difference hai? Deep explain karo.**

### ✅ **Answer:**

**Page Layout**

* Ye Salesforce Classic ke time ka core feature hai
* Isme sirf **fields, sections, related lists, buttons** control kar sakte ho
* Layout maximum **2-columns** hota hai
* Profile aur Record Type ke basis par assign hota hai
* Conditional visibility provide nahi karta

**Lightning Record Page (LRP)**

* Lightning App Builder ka part hai
* Fully component-based hota hai
* 1, 2, 3-column, tab-based, accordion-based layouts possible
* Dynamic visibility (if-this-then-display) rules support karta hai
* Page performance ko optimize kar sakte ho caching, regions, dynamic sections se
* Standard + Custom components add kar sakte ho

### **In short:**

* **Page Layout = Data ka structure** (fields, related lists
* **Lightning Record Page = UI ka structure** (components, layout design)

Dono milkar final Lightning Experience UI banate hain.

---

# **2️⃣ Ek object ke liye multiple page layouts kab aur kyu create karoge?**

### ✔ **Real Scenarios:**

1. **Different profiles**

   * Sales team: Deal-related fields
   * Support team: Case-handling fields

2. **Different regions**

   * US Layout
   * India Layout
   * Europe Layout

3. **Different record types**

   * Lead → Hot, Warm, Cold
   * Case → Technical Support, Billing Support

4. **Field visibility rules**

   * Beginner sales reps ko fewer fields
   * Managers ko advanced fields

5. **Different business processes**

   * Customer onboarding layout
   * Complaint resolution layout

### 🔥 **Why use multiple Page Layouts?**

* Business processes differ
* User experience optimized karna
* Training minimize karna
* Data entry fast karna

---

# **3️⃣ Page Layout performance issues kaise handle kiye hain?**

### **Performance Issues:**

* Too many fields (200+ visible fields)
* Too many related lists
* Sections ka heavy nesting
* Multiple record types ke conflicting fields
* Large formulas

### **Fix Strategies:**

✔ Unused fields layout se hatao
✔ Related lists ko limit karo (only needed ones)
✔ Lightning Record Page me

* Tabs
* Dynamic visibility
* Component level filtering use karo

✔ Duplicate layouts merge karo
✔ Compact layout optimize karo
✔ Page-level caching enable karo (LWCs)

### **Salesforce Recommendation:**

* **200 page layouts per object se zyada mat banao** — performance hit hota hai.

---

# **4️⃣ Page Layout, FLS, aur Record Types kaise interact karte hain?**

### **Hierarchy:**

1️⃣ **Field-Level Security (FLS)**

* Field dikhna hi nahi chahiye? → FLS hides it
* FLS > Page Layout

2️⃣ **Record Type**

* Page Layout assign karne ka base
* Different business processes control karta hai

3️⃣ **Page Layout**

* Fields ki position & UI control karta hai

### **Real Example**

A field layout me visible ho sakta hai → but FLS read-only ho to user edit nahi kar sakta.

---

# **5️⃣ Kaun se fields remove nahi kar sakte Page Layout se? Why?**

### ❌ **Fields that cannot be removed:**

* Name (Text/Auto Number)
* Owner
* Created By
* Last Modified By
* System-generated fields (Record ID, Last Activity, etc.)
* Standard required fields (Contact: Last Name)

### **Reason:**

Ye Salesforce ke **data model ka mandatory part** hain.
Inhe remove karne se record incomplete ho jayega.

---

# **6️⃣ Page Layout Required vs Field-Level Required vs Validation Rule — difference kya hai?**

### **1. Page Layout Required**

* Sirf UI level required
* API/import tools isko bypass kar sakte

### **2. Field-Level Required**

* Database-level required field
* API, code, integrations — sab me required hoga
* Strongest level of enforcement

### **3. Validation Rule Required**

* Conditional requirement
* Business logic-based
* Most flexible (ex: Stage = Closed Won → Amount required)

### **Best Practice:**

* Business logic? → Validation Rule
* Always required? → Field-Level required
* UI-only? → Page Layout required

---

# **7️⃣ Field visible hai par edit nahi ho raha — issue kahan hoga?**

### Possible causes:

1️⃣ **Field-Level Security (FLS) = Read Only**
2️⃣ **Profile permissions me Edit off**
3️⃣ **Record-level sharing me no write access**
4️⃣ **Page Layout me field read-only mark kiya**
5️⃣ **Field formula field ho (always read-only)**

### Most senior-level answer:

*"First FLS check karta hoon. Layout read-only tabhi effect karega jab FLS editable ho."*

---

# **8️⃣ 250+ Page Layouts ho gaye hain. Kaise optimize karoge?**

### Solutions:

✔ Record types reduce karo
✔ Duplicate layouts merge karo
✔ Profiles simplify karo
✔ Dynamic forms + Lightning Record Page introduce karo
✔ Users ke process simplify karo
✔ Unused layouts delete karo
✔ Global actions + Quick actions use karo

---

# **9️⃣ Related lists customization me kya-kya kar sakte ho?**

### You can modify:

✔ Visible columns
✔ Related list order
✔ Buttons (New, Edit, Delete)
✔ Link position
✔ Sort order
✔ Enhanced related list filters (Lightning)

---

# **🔟 Clone button ko modify kaise karte ho?**

### Options:

✔ Remove from Page Layout
✔ Custom Clone button using:

* Flow
* Screen Flow
* Apex
  ✔ Lightning Action create karna
  ✔ JavaScript button (Classic only)

---

# **1️⃣1️⃣ Page Layout assignment priority kya hoti hai?**

### Priority:

1️⃣ Record Type
2️⃣ User Profile
3️⃣ Default Layout

If Record Type assigned → Page Layout us basis par assign hota hai.

---

# **1️⃣2️⃣ Field Layout me visible hai but Lightning Page me nahi dikh raha, why?**

### Reasons:

* Field Lightning Page component ke andar add nahi kiya
* Dynamic visibility rule hide kar raha hai
* Tabs/Accordion ke andar hidden
* Wrong Lightning Page assigned
* FLS restrict
* Record type mismatch

---

# **1️⃣3️⃣ Page Layout se kya control nahi kar sakte?**

### Cannot control:

❌ Conditional visibility
❌ Component placement
❌ Dynamic UI rules
❌ Tab/Accordion layout
❌ LWCs placement
❌ Page performance

Ye sab Lightning Record Page se hota hai.

---

# **1️⃣4️⃣ Page Layout vs Dynamic Forms difference?**

### **Dynamic Forms Advantages:**

✔ Field-level conditional visibility
✔ Page sections ko component-wise show/hide
✔ Mobile/Desktop different UI
✔ Faster load time
✔ Field grouping per component

### Page Layout Limitations:

* 2-column only
* No conditional UI
* No component-level features

---

# **1️⃣5️⃣ Ek scenario jahan Page Layout ko replace karke Lightning Page use karoge?**

### Example:

Customer Service team →

* Case details only tab me
* Customer info second tab me
* SLA countdown component
* Chat history component
* Conditional components (Priority = High → Escalation component)

Page Layout ye nahi kar sakta.

---

# **1️⃣6️⃣ Dependent fields ko Page Layout me kaise organize karte ho?**

### Best Practices:

✔ Same section me rakho
✔ Child field after parent
✔ Clear section label: “Address Details”
✔ Use dynamic forms to show child field only when parent selected
✔ Keep validations consistent

---

# **1️⃣7️⃣ If a field is removed from layout but required at database level?**

### Result:

❌ User cannot create records
❌ Error: “Required field missing”
✔ Fix:

* Add field back OR
* Make default value OR
* Use automation to populate

---

# **1️⃣8️⃣ Standard buttons hide/enable kyu hote hain?**

### Rules:

* FLS decides edit/delete
* Org-wide sharing restrict delete
* Record type may disable convert
* Page layout can remove button
* Lightning Page can hide action region

---

# **1️⃣9️⃣ Page Layout vs FLS conflict scenario?**

### Example:

* Page layout → editable
* FLS → read-only

Result: User cannot edit field.

**Solution:**
FLS update karo (Profile/Permission Set se).

---

# **2️⃣0️⃣ Case Study: Support team ko Close Case button chahiye but Sales team ko nahi.**

### Solution:

✔ 2 Page Layouts banao→ Support Layout, Sales Layout
✔ Close Case button → Support Layout me add
✔ Sales Layout me remove
✔ Profiles assign:

* Support Profile → Support Layout
* Sales Profile → Sales Layout
