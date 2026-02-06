# Security : 

> **Salesforce Security is a layered mechanism to control user authentication, object access, field access, and record visibility.**

**Salesforce Security** ka matlab hota hai:

👉 **Right user ko, right data, right time par, right access dena**
aur baaki sab se data ko **protect** karna.

---

## 🔐 Org Level Security (Salesforce)

**Org Level Security** ka matlab hota hai:
👉 **poori Salesforce organization par apply hone wali security**
Iska focus hota hai **“kaun login kar sakta hai aur kaise”**, **data pe nahi**, balki **access pe**.

> 📌 Ye security **user ke login se pehle** ka control hota hai.

---

## 1️⃣ Maintain a list of authorized users

👉 Salesforce me **sirf wahi log login kar sakte hain**:

* Jo **User record active** ho
* Jinke paas **valid license** ho

### Example:

* Agar user **Inactive** hai ❌ → login nahi hoga
* Agar license remove kar diya ❌ → login block

📍 **Path**:
`Setup → Users → Users`

---

## 2️⃣ Set Password Policies

Tum decide kar sakte ho:

* Password ki **minimum length**
* **Complexity** (uppercase, lowercase, number, special char)
* Password **kitne din me expire** ho
* **Password history** (same password repeat na ho)

### Example:

* Password: minimum **8 characters**
* At least **1 capital + 1 number**
* Expiry: **90 days**

📍 **Path**:
`Setup → Password Policies`

---

## 3️⃣ Limit login to certain hours (Login Hours)

👉 User **sirf fixed time window** me login kar sake.

### Example:

* Office timing: **9 AM – 6 PM**
* 6 PM ke baad login ❌

📍 **Path**:
`Profile → Login Hours`

📌 Agar emergency ho → Admin **override** kar sakta hai.

---

## 4️⃣ Limit login from specific IP Addresses

👉 Tum decide kar sakte ho:

* **Kaunse IP range** se login allowed hai

### Example:

* Company network IP: `192.168.1.1 – 192.168.1.255`
* Bahar se login ❌

📍 **Path**:
`Profile → Login IP Ranges`

📍 **Path**:
`Setup → Network Access`

---

## 5️⃣ Restrict login locations (Trusted IP / Locations)

Salesforce check karta hai:

* New location / device se login
* Agar unknown ho → **OTP / verification** mangta hai

### Example:

* India se login OK ✅
* Foreign country se login → **Email/SMS verification**

📍 **Path**:
`Setup → Network Access`

---

## 🧠 Tumhare Notes ko Clean Summary me likhein

Tumhare notes ko interview-ready version me aise likh sakte ho 👇

> **Org Level Security in Salesforce controls who can log in to the Salesforce org and under what conditions. It includes user authentication, password policies, login hours, IP restrictions, and network access controls.**

---

## 🆚 Important Point (Interview Trick)

| Level                 | Controls         |
| --------------------- | ---------------- |
| Org Level Security    | **Login access** |
| Object Level Security | Object access    |
| Field Level Security  | Field visibility |
| Record Level Security | Data sharing     |

📌 **Org level kabhi bhi data visibility control nahi karta** ❌

---

## 🔥 Real Project Use Case

🏢 Company rule:

* Login only from office IP
* Working hours: 10–7
* Strong password mandatory

➡️ Sab cheezein **Org Level Security** se implement hongi.

---
---
---


## 🔐 Object Level Security (OLS) — Salesforce

**Object Level Security** ye decide karti hai ki
👉 **user kisi object (Account, Contact, Custom Object, etc.) par kya-kya kar sakta hai**

Matlab:

* Object **dekh sakta hai ya nahi**
* Record **create / edit / delete** kar sakta hai ya nahi

Ye sab **Salesforce** me **Profiles aur Permission Sets** se control hota hai.

---

## 🎯 OLS (Object Level Security) kya control karta hai?

Object level pe sirf ye 4 cheezein hoti hain:

| Permission | Meaning                     |
| ---------- | --------------------------- |
| Read       | Records dekh sakta hai      |
| Create     | Naye records bana sakta hai |
| Edit       | Existing records update     |
| Delete     | Records delete              |

📌 **Agar Read hi nahi hai → baaki sab automatically useless ho jaate hain**

---

## 📍 OLS kaha se set hoti hai?

### 1️⃣ Profile se (Primary control)

📍 Path:
`Setup → Profiles → (Select Profile) → Object Settings`

Har object ke liye checkboxes:

* Read
* Create
* Edit
* Delete
* View All
* Modify All

### Example:

**Sales User Profile**

* Account: Read, Create, Edit ✅
* Delete ❌

- ➡️ Sales user account bana & edit kar sakta hai
- ➡️ Delete button dikhega hi nahi

---

### 2️⃣ Permission Set se (Extra access dene ke liye)

👉 Jab kisi ek user ko **profile se zyada power** deni ho.

📍 Path:
`Setup → Permission Sets → Object Settings`

### Example:

* Profile: Contact Read only
* Permission Set: Contact Edit

➡️ User **edit bhi kar paayega**

📌 **Permission Set kabhi permission remove nahi karta, sirf add karta hai**

---

## 🧠 View All vs Modify All (IMPORTANT)

| Permission | Power                                       |
| ---------- | ------------------------------------------- |
| View All   | Sab records dekh sakta hai (sharing ignore) |
| Modify All | Sab records edit + delete (super power)     |

📌 Ye **Record Level Sharing ko override** kar dete hain.

---

## 🧩 Custom Object Example

Custom Object: `Invoice__c`

| User         | Permission         |
| ------------ | ------------------ |
| Finance User | Read, Create, Edit |
| Sales User   | Read only          |
| Intern       | No access          |

➡️ Jisko access nahi → object hi visible nahi hoga tab bar me

---

## 🚫 Common Confusion (Interview Favorite)

❓ *Agar user ko Object access nahi hai to?*

✔️ Object:

* Tab visible ❌ (nahi)
* Reports me use ❌ (nahi)
* API se access ❌ (nahi)
* SOQL query ❌ (nahi)

---

## 🔁 OLS vs FLS (Quick Diff)

| Feature | Object Level             | Field Level               |
| ------- | ------------------------ | ------------------------- |
| Control | Object                   | Field                     |
| Example | Account Edit             | Account.Revenue Read only |
| Where   | Profile / Permission Set | Same                      |

📌 **Flow**:
**Org → Object → Field → Record**

---

## 🏢 Real Project Scenario

Company rule:

* Intern user:

  * Account ❌
  * Contact Read only
* Manager:

  * Account Full access
  * Contact Full access

➡️ Ye sab **Object Level Security** se hi hota hai.

---

## 📝 Interview Ready Definition

> **Object Level Security in Salesforce controls what actions a user can perform on an object, such as read, create, edit, and delete. It is managed using profiles and permission sets and applies uniformly across all records of that object.**

---
---
---


## 🔐 Field Level Security (FLS) — Salesforce

**Field Level Security** ye decide karti hai ki
👉 **user kisi object ke kaun-kaun se fields dekh sakta hai aur edit kar sakta hai**

📌 Object ka access ho sakta hai, lekin **field hide / read-only** ho sakta hai.

Example:
User ko **Account** dikhta hai ✅
Lekin **Annual Revenue** field ❌

---

## 🎯 FLS kya control karta hai?

Har field ke liye sirf **2 permissions** hote hain:

| Permission  | Meaning        |
| ----------- | -------------- |
| Read Access | Field visible  |
| Edit Access | Field editable |

📌 **Edit = Read automatically**
📌 **Read ke bina Edit possible hi nahi**

---

## 📍 FLS kaha se set hoti hai?

### 1️⃣ Profile ke through

📍 Path:
`Setup → Profiles → (Profile Name) → Object Settings → (Object) → Field Permissions`

Yahan har field ke aage:

* Read
* Edit checkbox

### Example:

**Sales Profile**

* Annual Revenue → Read only
* Rating → Read + Edit

---

### 2️⃣ Permission Set ke through (MOST COMMON IN PROJECTS)

📍 Path:
`Setup → Permission Sets → Object Settings → Field Permissions`

### Example:

* Profile: Salary__c field hidden
* Permission Set: Salary__c Read + Edit

➡️ Sirf selected users ko field dikhegi

📌 **Permission Set kabhi field hide nahi karta, sirf extra access deta hai**

---

## 🔁 Profile vs Permission Set (FLS POV)

| Case                  | Result               |          |
| --------------------- | -------------------- | -------- |
| Profile: No Read      | Field hidden         |          |
| Permission Set: Read  | Field visible        |          |
| Profile: Read only    | Permission Set: Edit | Editable |
| Permission Set remove | Back to profile      |          |

---

## 🚫 Important Rule (Golden Rule)

> ❗ **No Object Access = No Field Access**

Agar:

* Object ka Read ❌
  ➡️ Field FLS meaningless ❌

---

## 🧠 Visual Flow (Yaad rakhne ka trick)

👉 **User sees a field only if ALL are true**:

1. Org access ✅
2. Object Read access ✅
3. Field Read access ✅
4. Record access (sharing) ✅

❌ Kahin bhi fail → field invisible

---

## 🧩 Standard vs Custom Fields

| Field Type     | FLS           |
| -------------- | ------------- |
| Standard Field | Yes           |
| Custom Field   | Yes           |
| Formula Field  | Read only     |
| Auto Number    | Read only     |
| System Fields  | Mostly hidden |

---

## ⚠️ FLS & Apex / SOQL (VERY IMPORTANT)

❌ Apex **by default FLS ignore karta hai**

### Bad Code:

```apex
Account a = [SELECT AnnualRevenue FROM Account LIMIT 1];
```

### Good Code:

```apex
if (Schema.sObjectType.Account.fields.AnnualRevenue.isAccessible()) {
   // safe to use
}
```

OR (Best Practice)

```apex
SELECT AnnualRevenue FROM Account
WITH SECURITY_ENFORCED
```

📌 Interview me ye bolna **brownie points** deta hai 🍫

---

## ⚠️ FLS & Reports / UI

| Area        | FLS Applied?        |
| ----------- | ------------------- |
| Standard UI | ✅                   |
| Reports     | ✅                   |
| List Views  | ✅                   |
| Flow        | ✅                   |
| Apex        | ❌ (manual)          |
| API         | ❌ (unless enforced) |

---

## 🏢 Real Project Scenario

🏦 Banking App:

* Object: Customer__c
* Field: PAN_Number__c

| User    | Access      |
| ------- | ----------- |
| Agent   | Hidden      |
| Manager | Read only   |
| Admin   | Read + Edit |

➡️ Perfect use case of **Field Level Security**

---

## 📝 Interview-Ready Definition

> **Field Level Security in Salesforce controls the visibility and editability of individual fields on an object. It ensures that users only see and modify fields they are authorized to access, and it is enforced through profiles and permission sets.**

---

## 🔥 Common Interview Traps

❓ *Field visible but editable nahi — why?*
✔️ Edit access missing

❓ *Permission Set add karne ke baad bhi field hidden?*
✔️ Object Read missing

❓ *Apex me field hidden hone ke bawajood data aa raha?*
✔️ FLS enforce nahi ki

---
---
---


## 🔐 Profiles

**Profile** ye define karta hai:

> 👉 **User Salesforce me kya kar sakta hai aur kya nahi (baseline access)**

Har user ke paas **exactly ONE profile hota hai** (mandatory).

📌 Profile = **Minimum permissions**
📌 Permission Set = **Extra permissions**

---
---
> Jab hum first time kisi profile ko open karenge to UI different ho skta hai usko enhange krne ke liye hame Setup -> User Management Setting -> Enhange Profile User Interface (Toggle On) krna hota hai.
---
---

## 🎯 Profile kya-kya control karta hai?

Profiles **sirf data nahi**, balki **system behavior** bhi control karte hain.


### 🔑 1. Object Level Security (OLS)

* Read
* Create
* Edit
* Delete
* View All
* Modify All

Example:

* Sales Profile → Account Read, Create, Edit
* Delete ❌

---

### 🔑 2. Field Level Security (FLS)

* Field visible?
* Field editable?

Example:

* Salary__c → Hidden for Sales
* Visible for Manager

---

### 🔑 3. Record Level Entry Points

Profile **directly sharing nahi karta**, but:

* **Role assign karne ka base** deta hai
* Tab visibility se record access affect hota hai

📌 Actual sharing → OWD, Roles, Sharing Rules (not profile)

---

### 🔑 4. App, Tab & Page Access

* Kaunsa App dikhega
* Kaunsa Tab visible / hidden
* Default landing tab

Example:

* Sales app visible
* Service app hidden

---

### 🔑 5. System Permissions (VERY IMPORTANT)

Ye permissions profile ka **danger zone** hota hai 😄

Some powerful permissions:

* Modify All Data
* View All Data
* Customize Application
* Run Reports
* Export Reports
* Data Import Wizard
* Author Apex

📌 Galat profile = security breach risk ❌

---

### 🔑 6. Login & Session Controls

Profile se:

* Login Hours
* Login IP Ranges

Example:

* Intern profile → 10 AM–6 PM
* Admin → 24x7

---

## 🧠 Standard Profiles vs Custom Profiles

| Point         | Standard | Custom |
| ------------- | -------- | ------ |
| Editable      | ❌        | ✅      |
| Recommended   | ❌        | ✅      |
| Real Projects | Rare     | Always |

📌 **Golden Rule**:
❌ Never modify Standard Profile
✅ Clone → Custom Profile

---

### “View All” ka exact matlab kya hota hai?

#### 🔍 View All = Object ke **saare records dekh sakta hai**

Agar kisi user ko kisi object par **View All** mil gaya:

* User **us object ke saare records dekh sakta hai**
* Chahe:

  * Record uska na ho
  * Role ke bahar ka ho
  * Sharing rule se share na hua ho

👉 **Sharing completely bypass ho jati hai (Read level par)**

##### Example:

* Account OWD = **Private**
* Normally user sirf apne accounts dekhta hai
* Lekin agar **Account par View All** diya:

  * User **system ke saare Accounts dekh sakta hai**

📌 **View All = Read access without sharing**

---

### “Modify All” ka exact matlab kya hota hai?

#### ✏️ Modify All = Object ke **saare records pe full control**

Agar kisi user ko **Modify All** mil gaya:

* User:

  * Saare records **dekh sakta hai**
  * Saare records **edit kar sakta hai**
  * Saare records **delete kar sakta hai**
* Ownership ya sharing ka koi matter nahi

👉 **Sharing completely bypass ho jati hai (Read + Write + Delete)**

📌 **Modify All = Full access without sharing**

---

#### Important Interview Points ⭐

* **View All / Modify All = Object level power**
* Ye **Manual Sharing, Role Hierarchy, OWD sab bypass** kar dete hain
* Ye **“Grant Access Using Hierarchies”** se bhi zyada powerful hote hain
* Normally **Profiles pe kam use**, Permission Sets pe dena best practice

---


## 🏗️ Profile Design Best Practice (REAL PROJECT)

### ❌ Old Style (Bad Practice)

* 10 profiles for 10 variations
* Maintenance nightmare 😵

### ✅ New Style (Best Practice)

* Few Profiles (Job based)

  * Sales User
  * Support User
  * Manager
* Variations handled by **Permission Sets**

📌 Salesforce khud recommend karta hai:

> **“Use Permission Sets for flexibility, Profiles for baseline.”**

---

### 🧩 Profile + Permission Set (Security Formula)

```text
Final User Access =
Profile permissions
+ Permission Set permissions
```

❌ Permission Set kabhi bhi:

* Permission remove nahi karta
* Restriction nahi lagata

---

## ⚠️ Common Security Mistakes (Interview Gold)

### ❌ Giving “Modify All Data” unnecessarily

→ User sab data edit/delete kar sakta hai

### ❌ Too many profiles

→ Hard to manage, bugs increase

### ❌ Profile used for temporary access

→ Permission Set hona chahiye tha

---

## 🔄 Profile vs Role (Clear Confusion)

| Profile          | Role                       |
| ---------------- | -------------------------- |
| Mandatory        | Optional                   |
| Permission based | Data visibility            |
| What user can do | Which records user can see |

📌 Role ≠ Security baseline
📌 Profile = Security baseline

---

## 🏢 Real Project Example

Company roles:

* Sales Rep
* Sales Manager
* Admin

### Design:

**Profiles**

* Sales User (basic)
* Manager User
* System Admin

**Permission Sets**

* Discount Approval
* Export Reports
* Special Object Access

➡️ Clean, scalable & secure system ✅

---

## 📝 Interview-Ready Definition

> **A Profile in Salesforce defines the baseline level of access a user has, including object permissions, field-level security, system permissions, app and tab visibility, and login restrictions. Every user must be assigned exactly one profile.**

---

## 🔥 Rapid-Fire Interview Q&A

❓ Can a user have multiple profiles?
❌ No (only one)

❓ Can a Permission Set override profile restrictions?
❌ It can only add, not remove

❓ Profiles control record sharing?
❌ No (OWD & Sharing Rules do)

❓ Best practice: more profiles or more permission sets?
✅ Fewer profiles, more permission sets

---

### 🧠 Memory Trick (1 line)

> **Profile = “Base access”
> Permission Set = “Extra power”**

---
---
---
---

## 🔐 Permission Sets in Salesforce

**Permission Set** ka simple meaning:

> 👉 **Profile ke upar extra permissions add karna (without changing profile)**

- 📌 Permission Set **baseline nahi hota**
- 📌 Ye **Profile ko override nahi karta**, sirf **extend** karta hai

Ye concept **Salesforce** ka **best practice standard** ban chuka hai.

---

### 🧠 Permission Set kyun introduce hua?

### ❌ Old problem (Profiles only):

* Har choti requirement ke liye **new profile**
* 20 users → 20 profiles 😵
* Maintenance nightmare

### ✅ Solution (Permission Sets):

* **Few profiles**
* **Many permission sets**
* Flexible & scalable design ✅

---

## 🎯 Permission Set kya-kya control karta hai?

Almost **sab kuch**, jo profile karta hai (except few things):

### 🔑 1️⃣ Object Level Security (OLS)

* Read / Create / Edit / Delete
* View All / Modify All

Example:
- Profile → Account Read
- Permission Set → Account Edit
- ➡️ Final = Read + Edit

---

### 🔑 2️⃣ Field Level Security (FLS)

* Field visibility
* Field editability

Example:
- Profile → Salary__c hidden
- Permission Set → Salary__c Read + Edit
- ➡️ Field visible & editable

---

### 🔑 3️⃣ System Permissions

Bahut powerful hoti hain ⚠️

Examples:

* Run Reports
* Export Reports
* Data Import Wizard
* Create Reports & Dashboards
* Author Apex (Dev only)

📌 Real projects me mostly **system permissions Permission Set se** di jati hain.

---

### 🔑 4️⃣ App & Tab Access

* Extra App visible
* Extra Tabs visible

Example:

* Profile → Only Sales App
* Permission Set → Service App access

---

### 🔑 5️⃣ Apex Class / VF Page Access

* Controller access
* Visualforce page access

📌 Without this → runtime error aata hai even if object access hai.

---

## 🚫 Permission Set kya **NAHI** karta?

❌ Ye cheezein Permission Set control nahi karta:

| Feature             | Controlled By       |
| ------------------- | ------------------- |
| Login Hours         | Profile             |
| Login IP Ranges     | Profile             |
| Password Policies   | Org Level           |
| Record Sharing      | OWD / Sharing Rules |
| Restrict permission | ❌ Not possible      |

📌 **Golden Rule**:

> Permission Set kabhi bhi **permission remove nahi karta**

---

## 🔁 Multiple Permission Sets (VERY IMPORTANT)

✔️ Ek user ke paas:

* 1 Profile (mandatory)
* **Multiple Permission Sets** ho sakte hain

### Example:

User = Sales Executive

Assigned:

* Base Profile: Sales User
* Permission Set 1: Discount Approval
* Permission Set 2: Export Reports
* Permission Set 3: Special Object Access

➡️ Final access = sab ka **combined power**

---

## 🧮 Final Access Formula (Yaad rakhna 🔥)

```text
User Access =
Profile
+ Permission Set A
+ Permission Set B
+ Permission Set C
```

❌ Kabhi minus nahi hota
✅ Sirf plus hota hai

---

## 🏗️ Types of Permission Sets

### 1️⃣ Permission Set (Normal)

* Single permission bundle

### 2️⃣ Permission Set Group (Advanced)

* Multiple permission sets ka group

Example:

* Sales_Power_User_Group

  * Discount_PS
  * Export_PS
  * Advanced_Reports_PS

➡️ Ek click me sab assign

📌 Enterprise projects me common hai.

---

## 🏢 Real Project Scenario (Must Read)

🏦 Banking Project:

### Profiles:

* Bank User
* Bank Manager

### Permission Sets:

* KYC_Edit_Access
* PAN_Field_Access
* Export_Reports
* Approval_Access

➡️ Jab manager promotion mile:

* Profile same
* Extra Permission Set assign
  ✅ Clean & safe design

---

## ⚠️ Common Mistakes (Interview Gold)

❌ Permission Set ko restriction ke liye use karna
❌ Temporary access ke liye profile change karna
❌ System permissions directly profile me dena
❌ Too many profiles banana

---

## 📝 Interview-Ready Definition

> **A Permission Set in Salesforce is a collection of settings and permissions that extends a user’s access beyond their profile. It is used to grant additional object, field, system, and application permissions without changing the user’s profile.**

---

## 🔥 Rapid Interview Q&A

❓ Can Permission Set remove access given by profile?
❌ No

❓ Can user have multiple Permission Sets?
✅ Yes

❓ Best practice: Profiles or Permission Sets?
✅ Few profiles + many permission sets

❓ Login IP restriction Permission Set se possible?
❌ No (Profile only)

---

## 🧠 One-Line Memory Trick

> **Profile = Minimum access**
> **Permission Set = Extra power when needed**

---


### 🧠 Easy yaad rakhne ka trick

* **Records** → *Sharing / OWD*
* **Object / Field** → *Profile / Permission Set*

### 🎯 One-line summary

* **Record security** = *Kaunsa record dikhe*
* **Object/Field security** = *Kya cheez dikhe aur edit ho*

---
---
---
---

🔥 Excellent — **Permission Set Groups (PSG)** Salesforce security ka **advanced + enterprise-level** topic hai. Ye cheez samajh aagayi to tum **architect-level thinking** dikha sakte ho interview me 💪

Chalo **deep dive + real project use cases + traps** ke saath karte hain.

---

## 🔐 Permission Set Groups (Deep Dive)

**Permission Set Group** ka simple meaning:

> 👉 **Multiple Permission Sets ko ek logical group me bundle karna**

📌 User ko group assign karo →
📌 Salesforce automatically **andar ke sab Permission Sets assign** kar deta hai.

Ye feature **Salesforce** me **large orgs ke liye design** kiya gaya hai.

---

## ❓ Permission Set Groups kyun aaye?

### ❌ Problem (Multiple Permission Sets)

* Ek user ko 6–7 permission sets
* Hard to track ❌
* Admin ke liye confusion 😵

### ✅ Solution (Permission Set Groups)

* 1 group assign
* Logical role-based access
* Easy onboarding & offboarding ✅

---

## 🧠 Permission Set Group ka structure

```text
Permission Set Group
 ├── Permission Set A (Object Access)
 ├── Permission Set B (Field Access)
 ├── Permission Set C (System Permissions)
 └── Permission Set D (Apex Access)
```

➡️ User ko **sab ka combined access**

---

## 🎯 PSG kya-kya control karta hai?

Jo kuch **Permission Set** karta hai, wahi PSG bhi karta hai:

* Object Level Security
* Field Level Security
* System Permissions
* App & Tab Access
* Apex / VF access

📌 PSG khud permission define nahi karta
📌 Ye **sirf container** hota hai

---

## 🔑 Muting Permission Set (VERY IMPORTANT)

### Rule yaad rakho:

> ❌ **Permission Set kabhi permission remove nahi karta**

Matlab:

* Profile ya Permission Set ne agar koi permission de di
* To **dusra Permission Set use hata nahi sakta**

👉 Yahin par **Muting** aata hai 🔥

---

### 🔕 Muting Permission Set kya hota hai?

**Muting Permission Set** ka matlab:

> 👉 **Permission Set Group ke andar kisi specific permission ko OFF kar dena**

📌 Ye kaam **sirf Permission Set Group ke andar** hota hai
📌 Normal Permission Set se **kabhi bhi** permission remove nahi hota

---

### ⚠️ Sabse important rule (Golden Rule)

> ❗ **Muting sirf wahi permissions hata sakta hai
> jo Permission Set Group ke andar ke Permission Sets se aayi ho**

❌ Profile wali permission mute nahi hoti


---

## 🧠 PSG vs Permission Set (Clear Diff)

| Feature         | Permission Set | Permission Set Group |
| --------------- | -------------- | -------------------- |
| Standalone      | Yes            | No                   |
| Multiple bundle | ❌              | ✅                    |
| Muting support  | ❌              | ✅                    |
| Enterprise use  | Medium         | High                 |

---

## 🏗️ How to create Permission Set Group

📍 Path:
`Setup → Permission Set Groups → New`

Steps:
- 1️⃣ Group name
- 2️⃣ Add Permission Sets
- 3️⃣ Save
- 4️⃣ **Calculate Group** (IMPORTANT ⚠️)
- 5️⃣ Assign to user

📌 Jab bhi PS change ho → **Recalculate mandatory**

---

## 🏢 Real Project Use Cases (VERY IMPORTANT)

### 🏦 Banking Project

#### Permission Sets:

* Account_Read_PS
* KYC_Edit_PS
* PAN_Field_PS
* Export_Reports_PS

#### Permission Set Group:

**Bank_Manager_PSG**

➡️ New manager join:

* Assign 1 PSG
* No manual PS selection
* Zero mistake ✅

---

### 🏥 Healthcare Project

#### PSG:

**Doctor_PSG**

* Patient_Record_PS
* Prescription_Edit_PS
* Appointment_PS

**Nurse_PSG**

* Patient_Read_PS
* Appointment_PS

- ➡️ Role change → PSG swap
- ➡️ Clean audit trail

---

## 🔄 Onboarding / Offboarding Magic ✨

### Onboarding:

* Assign Profile
* Assign PSG
* Done in 2 minutes 🚀

### Offboarding:

* Remove PSG
* User loses all extra access immediately 🔒

---

## ⚠️ Common Mistakes (Interview Gold)

- ❌ PSG ko base security banana
- ❌ Profile me zyada power dena
- ❌ Muting feature ignore karna
- ❌ Recalculate bhool jana

---

## 📝 Interview-Ready Definition

> **A Permission Set Group in Salesforce is a collection of permission sets that can be assigned together to users. It simplifies permission management and supports muting permissions to fine-tune access in complex security models.**

---

## 🔥 Rapid Interview Q&A

- ❓ Can PSG exist without Permission Sets?
- ❌ No

<br/>

- ❓ Can PSG remove profile permission?
- ❌ Yes (using Muting)

<br/>

- ❓ Can user have multiple PSGs?
- ✅ Yes (but design carefully)

<br/>

- ❓ Recalculate kyun important hai?
- ✔️ Effective permissions update ke liye

---

## 🧠 Memory Trick

> - **Permission Set = Building block 🧱**
> - **Permission Set Group = Lego set 🧩**

---
---
---
---


# 🧠 Tricky Interview Scenarios (Real + Confusing Ones)

## 🔥 Scenario 1: Permission Set remove karke bhi access ja raha nahi

### ❓ Question:

User ke paas **Export Reports** access aa rahi hai.
Maine Permission Set remove kar diya, fir bhi access aa rahi hai. Why?

### ✅ Answer:

Kyuki:

* Permission **Profile se** aa rahi hai
* Permission Set sirf add karta hai, remove nahi

📌 **Fix**:

* Profile se permission hatao
* Ya future ke liye: system permissions profile me dena hi nahi

---

## 🔥 Scenario 2: Muting kiya but permission still aa rahi

### ❓ Question:

Permission Set Group me maine **Export Reports mute** kiya,
but user ke paas fir bhi access aa rahi hai.

### ✅ Answer:

2 possible reasons (interviewer ko dono batao):

1️⃣ Permission **Profile se aa rahi hai**
👉 Muting profile ko affect nahi karta

2️⃣ PSG **Recalculate** nahi kiya
👉 Old permissions still active

📌 Interview punch line:

> “Muting works only on permissions coming from permission sets inside the group.”

---

## 🔥 Scenario 3: Field visible hai but edit nahi ho rahi

### ❓ Question:

User ko field dikh rahi hai, lekin wo edit nahi kar pa raha. Why?

### ✅ Answer:

* Field **Read access** hai
* But **Edit access** missing hai (Profile ya PS me)

📌 Bonus point:

> “Edit permission always requires Read permission.”

---

## 🔥 Scenario 4: Object access hai but tab hi nahi dikh rahi

### ❓ Question:

Account object ka Read access hai,
but Account tab visible nahi hai.

### ✅ Answer:

* Tab visibility → **Profile / Permission Set**
* Object permission ≠ Tab visibility

📌 Fix:

* Profile → Tab Settings → Default On

---

## 🔥 Scenario 5: Apex me data aa raha hai, UI me nahi

### ❓ Question:

Field UI me hidden hai (FLS),
but Apex SOQL me data aa raha hai. Why?

### ✅ Answer:

* Apex **by default FLS ignore karta hai**

📌 Correct practice:

```sql
WITH SECURITY_ENFORCED
```

or `Schema.isAccessible()`

---

## 🔥 Scenario 6: Too many profiles issue

### ❓ Question:

Org me 25 profiles hain, manage karna mushkil ho raha. Solution?

### ✅ Answer:

* Reduce profiles (job-based)
* Use Permission Sets + PSG
* Use Muting for exceptions

📌 Architect-level answer ✅

---

## 🏗️ PART 2: End-to-End Security Example

(Profile + PS + PSG + Muting)

Ye **complete real project story** hai — interview me bol sakte ho.

---

## 🏦 Project: Banking Application

### 👥 Users:

* Bank Agent
* Bank Manager
* Junior Manager

---

## 1️⃣ Profile (Baseline Access)

### Profile: **Bank_User_Profile**

✔ Object Access:

* Account → Read
* Contact → Read

✔ Field Access:

* PAN__c → Hidden
* Salary__c → Hidden

✔ System Permissions:

* ❌ Export Reports
* ❌ Delete Records

📌 Profile = **minimum safe access**

---

## 2️⃣ Permission Sets (Building Blocks)

### PS_Account_Edit

* Account → Edit

### PS_KYC_Edit

* PAN__c → Read + Edit

### PS_Export

* Export Reports ✅

---

## 3️⃣ Permission Set Group (Role Based)

### PSG: **Bank_Manager_PSG**

Includes:

* PS_Account_Edit
* PS_KYC_Edit
* PS_Export

➡️ Bank Manager ko full power chahiye

---

## 4️⃣ Special Case (Muting in Action 🔥)

### 👤 Junior Manager

* Account edit chahiye ✅
* KYC edit chahiye ✅
* Export reports ❌ (security risk)

### ❌ Problem:

PS_Export remove nahi kar sakte
(kyuki group me baaki permissions bhi chahiye)

---

## ✅ Solution: Muting Permission Set

PSG → **Muting Permission Set**

* Export Reports → ❌ muted

➡️ Junior Manager ka final access:

| Permission     | Result |
| -------------- | ------ |
| Account Edit   | ✅      |
| PAN Edit       | ✅      |
| Export Reports | ❌      |

🔥 Clean, scalable, no new profile, no new PS

---

## 🔁 Final Access Flow (One Line)

```text
Profile
+ Permission Sets
+ Permission Set Group
– Muted Permissions
= Final User Access
```

---

## 📝 Interview Closing Statement (POWERFUL)

Agar interviewer bole:

> “How do you design Salesforce security?”

Tum bolo:

> “I design security using minimal profiles for baseline access, permission sets for incremental permissions, permission set groups for role-based access, and muting permission sets to handle exceptions without creating new profiles or permission sets.”

💥 **Architect-level answer**

---
---
---
---

# 🔐 Record Level Security (Salesforce)

**Record Level Security** decide karti hai:

> 👉 **User kisi object ke kaun-kaun se records dekh / edit kar sakta hai**

- 📌 Ye **Object & Field security ke baad** apply hoti hai
- 📌 Ye **record-by-record** control hota hai

---

## 🧠 Security Order (yaad rakhna 🔥)

```text
Org
→ Profile / Permission Set
   → Object Level Security
     → Field Level Security
       → Record Level Security (OWD + Roles + Sharing)
```

---

# 1️⃣ OWD – Organization-Wide Defaults

**OWD** batata hai:

> 👉 **Default me ek user dusre user ke records dekh sakta hai ya nahi**

📍 Path:
`Setup → Sharing Settings`

---

## 🔑 OWD Access Levels

| Level                | Meaning                         |
| -------------------- | ------------------------------- |
| Private              | Sirf owner + explicit sharing   |
| Public Read Only     | Sab dekh sakte, edit sirf owner |
| Public Read/Write    | Sab dekh + edit                 |
| Controlled by Parent | Parent object decide kare       |

📌 OWD hamesha **most restrictive** se start hota hai

---

## 🧩 Example (Account OWD = Private)

* User A creates Account A1
* User B ❌ cannot see A1 (default)

➡️ Ab access dene ke liye **Roles / Sharing Rules** chahiye

---

# 2️⃣ Roles (Hierarchy Access)

**Roles** ka kaam:

> 👉 **Hierarchy ke through records ka access dena**

📍 Path:
`Setup → Roles`

---

## 🧠 Role Hierarchy Rule

> **Managers automatically see subordinates’ records**

Example:

```
CEO
 └─ Manager
     └─ Sales Rep
```

* Sales Rep ka record → Manager & CEO dekh sakte hain
* Manager ka record → CEO dekh sakta hai

📌 Ye **Profile se independent** hota hai

---

## ⚠️ Important Role Settings

### Grant Access Using Hierarchies

* Default: ON
* Custom object me OFF bhi kar sakte ho

➡️ Tab role hierarchy ka effect nahi padega

---

# 3️⃣ Sharing (Actual Record Access)

OWD restrictive hai → Sharing se relax hota hai

---

## 🔁 Types of Sharing

### 1️⃣ Role-Based Sharing Rule

* Role → Role access

Example:

* Sales Rep records → Sales Manager

---

### 2️⃣ Public Group Sharing Rule

* Group → Role / Group / User

Example:

* Finance Group → All Accounts (Read)

---

### 3️⃣ Owner-Based Sharing

* Record owner ke basis pe

Example:

* Owner = Sales Rep → Share with Manager

---

### 4️⃣ Criteria-Based Sharing

* Record field condition pe

Example:

* Region = “North” → North Team

🔥 Interview favorite

---

### 5️⃣ Manual Sharing

* Record level pe manually share

📌 Sirf:

* Owner
* Admin
* Modify All users

---

### 6️⃣ Apex Managed Sharing

* Code ke through dynamic sharing

Example:

```apex
AccountShare accShare = new AccountShare();
accShare.AccountId = acc.Id;
accShare.UserOrGroupId = userId;
accShare.AccountAccessLevel = 'Edit';
insert accShare;
```

---

# 🧩 Real Project End-to-End Example

## 🏦 Banking App – Customer Records

### Object: Customer__c

### Step 1️⃣ OWD

* Customer__c = Private

---

### Step 2️⃣ Roles

```
Branch Head
 └─ Branch Manager
     └─ Relationship Manager
```

➡️ Manager sees RM records automatically

---

### Step 3️⃣ Sharing Rules

#### Criteria Based Sharing

* If `Customer_Type__c = VIP`
* Share with → VIP Team (Read/Write)

---

### Step 4️⃣ Manual Sharing

* Temporary access to Audit Team

---

### Final Result:

✔ Least privilege
✔ Controlled visibility
✔ Audit-friendly

---

# ⚠️ Common Interview Traps (VERY IMPORTANT)

### ❓ OWD Public Read Write hai, phir sharing rule ka kya kaam?

➡️ Koi kaam nahi (already open)

---

### ❓ Role hierarchy access kaise band karte?

➡️ Custom object → Grant Access Using Hierarchies = OFF

---

### ❓ Profile record access control karta hai?

❌ No (Profile sirf object/field)

---

### ❓ Permission Set sharing karta hai?

❌ No

---

# 📝 Interview-Ready Definition

> **Record Level Security in Salesforce controls which individual records a user can access. It is implemented using Organization-Wide Defaults, role hierarchy, and various sharing mechanisms such as sharing rules, manual sharing, and Apex managed sharing.**

---

# 🧠 One-Line Memory Trick

> **OWD = Default lock 🔒**
> **Roles = Vertical access ⬆️**
> **Sharing = Horizontal access ➡️**

---

## 🔥 Rapid Interview Q&A

* Most restrictive OWD? → **Private**
* Sharing rule can reduce access? → ❌
* Role mandatory? → ❌
* Apex sharing used when? → Dynamic logic

---
---
---
---



# 🔐 Record Level Security (Salesforce)

**Record Level Security** decide karti hai:

> 👉 **User kisi object ke kaun-kaun se records dekh / edit kar sakta hai**

📌 Ye **Object & Field security ke baad** apply hoti hai
📌 Ye **record-by-record** control hota hai

---

## 🧠 Security Order (yaad rakhna 🔥)

```text
Org
 → Profile / Permission Set
   → Object Level Security
     → Field Level Security
       → Record Level Security (OWD + Roles + Sharing)
```

---

## 1️⃣ OWD – Organization-Wide Defaults

**OWD** batata hai:

> 👉 **Default me ek user dusre user ke records dekh sakta hai ya nahi**

📍 Path:
`Setup → Sharing Settings`

---

## 🔑 OWD Access Levels

| Level                | Meaning                         |
| -------------------- | ------------------------------- |
| Private              | Sirf owner + explicit sharing   |
| Public Read Only     | Sab dekh sakte, edit sirf owner |
| Public Read/Write    | Sab dekh + edit                 |
| Controlled by Parent | Parent object decide kare       |

📌 OWD hamesha **most restrictive** se start hota hai

---

## 🧩 Example (Account OWD = Private)

* User A creates Account A1
* User B ❌ cannot see A1 (default)

➡️ Ab access dene ke liye **Roles / Sharing Rules** chahiye

---

## 2️⃣ Roles (Hierarchy Access)

**Roles** ka kaam:

> 👉 **Hierarchy ke through records ka access dena**

📍 Path:
`Setup → Roles`

---

## 🧠 Role Hierarchy Rule

> **Managers automatically see subordinates’ records**

Example:

```
CEO
 └─ Manager
     └─ Sales Rep
```

* Sales Rep ka record → Manager & CEO dekh sakte hain
* Manager ka record → CEO dekh sakta hai

📌 Ye **Profile se independent** hota hai

---

## ⚠️ Important Role Settings

### Grant Access Using Hierarchies

* Default: ON
* Custom object me OFF bhi kar sakte ho but standard object me OFF nahi kr skte.

➡️ Tab role hierarchy ka effect nahi padega

---

## 3️⃣ Sharing (Actual Record Access)

OWD restrictive hai → Sharing se relax hota hai

---

## 🔁 Types of Sharing

### 1️⃣ Role-Based Sharing Rule

* Role → Role access

Example:

* Sales Rep records → Sales Manager

---

### 2️⃣ Public Group Sharing Rule

* Group → Role / Group / User

Example:

* Finance Group → All Accounts (Read)

---

### 3️⃣ Owner-Based Sharing

* Record owner ke basis pe

Example:

* Owner = Sales Rep → Share with Manager

---

### 4️⃣ Criteria-Based Sharing

* Record field condition pe

Example:

* Region = “North” → North Team

🔥 Interview favorite

---

### 5️⃣ Manual Sharing

* Record level pe manually share

📌 Sirf:

* Owner
* Admin
* Modify All users

---

### 6️⃣ Apex Managed Sharing

* Code ke through dynamic sharing

Example:

```apex
AccountShare accShare = new AccountShare();
accShare.AccountId = acc.Id;
accShare.UserOrGroupId = userId;
accShare.AccountAccessLevel = 'Edit';
insert accShare;
```

---

# 🧩 Real Project End-to-End Example

## 🏦 Banking App – Customer Records

### Object: Customer__c

### Step 1️⃣ OWD

* Customer__c = Private

---

### Step 2️⃣ Roles

```
Branch Head
 └─ Branch Manager
     └─ Relationship Manager
```

➡️ Manager sees RM records automatically

---

### Step 3️⃣ Sharing Rules

#### Criteria Based Sharing

* If `Customer_Type__c = VIP`
* Share with → VIP Team (Read/Write)

---

### Step 4️⃣ Manual Sharing

* Temporary access to Audit Team

---

### Final Result:

- ✔ Least privilege
- ✔ Controlled visibility
- ✔ Audit-friendly

---

## ⚠️ Common Interview Traps (VERY IMPORTANT)

### ❓ OWD Public Read Write hai, phir sharing rule ka kya kaam?

➡️ Koi kaam nahi (already open)

---

### ❓ Role hierarchy access kaise band karte?

➡️ Custom object → Grant Access Using Hierarchies = OFF

---

### ❓ Profile record access control karta hai?

❌ No (Profile sirf object/field)

---

### ❓ Permission Set sharing karta hai?

❌ No

---

# 📝 Interview-Ready Definition

> **Record Level Security in Salesforce controls which individual records a user can access. It is implemented using Organization-Wide Defaults, role hierarchy, and various sharing mechanisms such as sharing rules, manual sharing, and Apex managed sharing.**

---

# 🧠 One-Line Memory Trick

> - **OWD = Default lock 🔒**
> - **Roles = Vertical access ⬆️**
> - **Sharing = Horizontal access ➡️**

---
---
---
---

# 🔐 OWD – Organization-Wide Defaults

**OWD** ka matlab:

> 👉 **Default me ek user dusre user ke records ko kitna access karega**

- 📌 Ye **record level** pe kaam karta hai
- 📌 Ye **baseline (most restrictive)** hota hai
- 📌 Baad me **Roles / Sharing** se access badhaya jata hai

Ye concept **Salesforce** ke security model ka **starting point** hai.

---

## 🧠 OWD ka simple thought

Socho company bolti hai:

> “By default, koi bhi dusre ka data na dekhe.
> Sirf jab zaroorat ho tab hi share karenge.”

➡️ **Yahi OWD hai**

---

## 📍 OWD kaha set hota hai?

`Setup → Sharing Settings → Organization-Wide Defaults`

Yahin se har object ke liye OWD define hota hai.

---

## 🔑 OWD Access Levels (DEEP)

### 1️⃣ **Private** (Most Restrictive 🔒)

👉 Sirf:

* Record Owner
* Admin
* Explicitly shared users

- ❌ Role hierarchy
- ❌ Sharing rules (jab tak define na ho)

**Use when**:

* Banking
* HR
* Medical
* Sensitive data

📌 **Best practice**:

> Hamesha **Private se start karo**

---

### 2️⃣ **Public Read Only**

👉 Sab users:

* Records **dekh** sakte hain
* Edit ❌ (sirf owner)

**Use when**:

* Reference data
* Read-only visibility chahiye

Example:

* Product Catalog
* Knowledge base records

---

### 3️⃣ **Public Read/Write**

👉 Sab users:

* Records dekh + edit

- ⚠️ **Danger zone**
- ❌ Sharing rules ka koi matlab nahi

**Use only when**:

* Truly open data
* Collaboration heavy object

---

### 4️⃣ **Controlled by Parent**

👉 Child object ka access
**Parent object ke OWD se control hota hai**

Example:

* Account → Contact
* Case → Case Comment
* Custom Parent → Custom Child

📌 Agar parent record ka access nahi →
child ka bhi nahi milega

---

## 🧩 OWD ka effect kaise kaam karta hai (Flow)

```text
User A creates record
        ↓
OWD check hota hai
        ↓
Dusre users ko default access milta hai
        ↓
Agar access kam hai
→ Roles / Sharing se open karte hain
```

---

## 🧠 OWD + Role Hierarchy relation

### Example:

OWD = Private

```
CEO
 └─ Manager
     └─ Sales Rep
```

* Sales Rep record → Manager & CEO dekh sakte hain (by role)
* Agar role hi assign nahi → koi access nahi

📌 **Role hierarchy OWD ko relax karta hai**

---

## ⚠️ Important OWD Rules (Interview Gold)

### ❗ Rule 1:

> OWD **kabhi bhi access increase nahi karta**,
> sirf **limit** karta hai.

---

### ❗ Rule 2:

> Sharing rules **access kam nahi kar sakte**,
> sirf badha sakte hain.

---

### ❗ Rule 3:

> OWD Public Read/Write hai
> → Sharing rules useless

---

### ❗ Rule 4:

> OWD har object ke liye **independent** hota hai

- Account = Private
- Contact = Public Read Only
- ✔ Totally valid

---

## 🏢 Real Project Example (Banking)

### Object: Customer__c

### Step 1️⃣ OWD

* Customer__c = **Private**

➡️ Default:
RM apne customers hi dekhe

---

### Step 2️⃣ Role Hierarchy

```
Branch Head
 └─ Branch Manager
     └─ RM
```

➡️ Manager apne RM ke customers dekhe

---

### Step 3️⃣ Sharing Rule

* Criteria:

  * Customer_Type = “VIP”
* Share with:

  * VIP Team (Read)

➡️ Controlled + secure visibility

---

## 🚫 Common Confusions (Clear karte hain)

### ❓ OWD profile se related hai?

❌ No (Profile = object/field)

---

### ❓ Permission Set OWD change kar sakta hai?

❌ Never

---

### ❓ Apex sharing OWD ko override karta hai?

❌ Nahi, sirf **explicit access add** karta hai

---

### ❓ OWD change karne se kya hota hai?

⚠️ **Recalculation hota hai**

* Large org me time lagta hai
* Temporary performance impact

---

## 📝 Interview-Ready Definition

> **Organization-Wide Defaults define the baseline level of record access for users in a Salesforce organization. They determine how records are shared by default and serve as the foundation for record-level security, which can then be expanded using role hierarchy and sharing rules.**

---

## 🧠 One-Line Memory Trick

> **OWD = Default lock 🔒**
> **Roles = Vertical unlock ⬆️**
> **Sharing = Horizontal unlock ➡️**

---
---
---
---

# 🔐 Role Hierarchy – Edge Cases

Role Hierarchy normally bolta hai:

> **Managers can see records owned by users below them**

…but real life me bahut saare **“BUT”** aate hain 😄
Ye sab **Salesforce** projects me frequently milte hain.

---

## 🔥 Edge Case 1: Role assign hi nahi hai

### ❓ Scenario

* User ke paas **Profile + Object access** hai
* But **Role blank** hai
* OWD = Private

### 👉 Result

❌ User kisi aur ka record **nahi dekh paayega**
❌ Manager bhi uske records **nahi dekhega**

### 🧠 Why?

Role hierarchy **sirf tab kaam karti hai jab role assigned ho**

📌 **Interview line**:

> “Without a role, users are isolated from the role hierarchy.”

---

## 🔥 Edge Case 2: OWD = Public Read/Write

### ❓ Scenario

* Object OWD = Public Read/Write
* Proper Role Hierarchy set hai

### 👉 Result

Role hierarchy ka **koi effect nahi**

### 🧠 Why?

* Data already open hai
* Role hierarchy sirf **restrictive OWD** me matter karti hai

📌 **Trap question**:
“OWD open hai, role hierarchy ka kya role?”

👉 **Answer: None**

---

## 🔥 Edge Case 3: Custom Object & “Grant Access Using Hierarchies” = OFF

### ❓ Scenario

* Custom Object: Invoice__c
* OWD = Private
* Role hierarchy defined
* BUT → **Grant Access Using Hierarchies = OFF**

### 👉 Result

❌ Manager **subordinate ke records nahi dekh paata**

### 🧠 Why?

Custom objects me role hierarchy **optional** hoti hai.

📌 **Interview gold**:

> “Role hierarchy can be disabled per custom object.”

---

## 🔥 Edge Case 4: Profile vs Role confusion

### ❓ Scenario

Interviewer puche:

> “Agar profile change kar do, kya record visibility badal jayegi?”

### 👉 Correct Answer

❌ No

### 🧠 Why?

* Profile → Object & Field
* Role → Record visibility

📌 **One-liner**:

> “Profiles control what you can do, roles control which records you see.”

---

## 🔥 Edge Case 5: Manager should NOT see subordinate data

### ❓ Scenario (Very common in banking/HR)

* RM ke records **manager ko nahi dikhne chahiye**
* OWD = Private
* But role hierarchy automatically access de rahi

### ✅ Solution options

- 1️⃣ Custom Object me
`Grant Access Using Hierarchies = OFF`
- 2️⃣ Roles ka use hi mat karo
- 3️⃣ Apex / Manual sharing use karo

📌 **Architect thinking** yahin dikhti hai.

---

## 🔥 Edge Case 6: Same role ≠ Same data access

### ❓ Scenario

* 2 users
* Same role
* OWD = Private

### 👉 Result

❌ Ek dusre ke records **nahi dikhenge**

### 🧠 Why?

Role hierarchy **vertical hoti hai**, horizontal nahi.

📌 Access ke liye:

* Sharing Rule
* Public Group
* Manual sharing

---

## 🔥 Edge Case 7: “Modify All” vs Role Hierarchy

### ❓ Scenario

* User ke paas `Modify All` permission hai
* OWD = Private
* Role bhi assigned hai

### 👉 Result

✅ User **sab records edit/delete** kar sakta hai
(Role hierarchy irrelevant)

### 🧠 Why?

System permissions **sharing model ko bypass** kar dete hain.

📌 Interview punch:

> “System permissions override record-level security.”

---

## 🔥 Edge Case 8: Apex Managed Sharing + Role Hierarchy

### ❓ Scenario

* OWD = Private
* Role hierarchy OFF (custom object)
* Apex sharing se access diya

### 👉 Result

- ✅ Sirf jisko share kiya, wahi access paayega
- ❌ Manager ko automatic access nahi

### 🧠 Why?

Apex sharing = **explicit sharing**, hierarchy independent.

---

## 🧠 Summary Table (Fast Revision)

| Situation                      | Role Hierarchy Works? |
| ------------------------------ | --------------------- |
| OWD = Private                  | ✅                     |
| OWD = Public RW                | ❌                     |
| No role assigned               | ❌                     |
| Custom object + hierarchy OFF  | ❌                     |
| Same role users                | ❌                     |
| System permission (Modify All) | ❌ needed              |

---

## 📝 Interview-Ready Power Statement

Agar interviewer bole:

> “Explain role hierarchy limitations”

Tum bolo:

> “Role hierarchy provides vertical record access only when OWD is restrictive and the object allows hierarchical access. It does not work for users without roles, for users at the same role level, or when overridden by system permissions or disabled on custom objects.”

💥 Strong answer.

---

## 🧠 Memory Trick

> - **Role = Vertical access only ⬆️**
> - **Same level = No sharing ↔️**
> - **System permission = God mode 😄**

---
---
---
---

# 🔐 Sharing Rules – Deep Dive (with Tricky Cases)

**Sharing Rules** ka kaam:

> 👉 **OWD se jo records hidden hain, unko automatically share karna**

📌 Sharing Rules **access kabhi kam nahi karte**
📌 Sirf **access increase** karte hain
📌 Ye **automated** hote hain (manual sharing nahi)

---

## 🧠 Pre-requisite (Interview Trap)

Sharing Rules tabhi kaam karte hain jab:

* OWD = **Private**
* ya **Public Read Only**

👉 OWD = Public Read/Write → Sharing rules useless ❌

---

# 1️⃣ Owner-Based Sharing Rules

### 🔍 Definition

> Records **record owner ke basis pe** share hote hain.

📍 Condition:

* Record owner ka **role / public group**

---

## 🧩 Owner-Based Sharing Example

### Scenario:

* Object: Account
* OWD = Private

Rule:

* IF **Owner Role = Sales Rep**
* Share with **Sales Manager Role** (Read)

➡️ Manager apne reps ke accounts dekhega

---

## 🔥 Owner-Based Tricky Cases

### ❓ Case 1: Owner ka role hi nahi

* Owner user ke paas **role blank**

👉 Rule **trigger hi nahi hoga**

📌 Interview line:

> “Owner-based sharing depends on owner’s role or group.”

---

### ❓ Case 2: Owner role change ho gaya

* Record owner same
* Owner ka role change

👉 Salesforce **sharing recalculate** karta hai

* Old sharing remove
* New sharing apply

📌 Performance impact ho sakta hai

---

### ❓ Case 3: Same role users

* User A & B same role
* OWD = Private

👉 Owner-based rule se **ek dusre ka data nahi milega**

📌 Rule vertical access ke liye hota hai

---

### ❓ Case 4: Manager should NOT see subordinate data

* OWD = Private
* Role hierarchy OFF (custom object)

👉 Owner-based sharing phir bhi kaam karega

📌 Ye role hierarchy se independent hai

---

# 2️⃣ Criteria-Based Sharing Rules

### 🔍 Definition

> Records **record ke field values ke basis pe** share hote hain.

📌 Owner se koi relation nahi

---

## 🧩 Criteria-Based Sharing Example

### Scenario:

* Object: Case
* OWD = Private

Rule:

* IF `Priority = High`
* Share with **Escalation Team** (Read/Write)

➡️ Auto escalation access

---

## 🔥 Criteria-Based Tricky Cases

### ❓ Case 1: Field value change ho jaye

* Priority = High → Low

👉 Sharing **automatically remove** ho jayegi

📌 Dynamic nature

---

### ❓ Case 2: Formula field used in criteria

* Criteria = Formula Field

👉 Rule **trigger hota hai**
BUT:

* Large org → performance hit

📌 Best practice:

> Avoid complex formulas in sharing rules

---

### ❓ Case 3: Multiple criteria rules overlap

* Rule A → Read
* Rule B → Read/Write

👉 **Highest access wins** (RW)

📌 Access kabhi reduce nahi hota

---

### ❓ Case 4: Criteria-based sharing & Role hierarchy OFF

* Custom object
* Hierarchy OFF

👉 Criteria sharing **phir bhi kaam karegi**

📌 Independent systems

---

## 🆚 Owner-Based vs Criteria-Based (Interview Table)

| Point              | Owner-Based       | Criteria-Based     |
| ------------------ | ----------------- | ------------------ |
| Based on           | Record owner      | Record field       |
| Dynamic on         | Owner role change | Field value change |
| Use case           | Team hierarchy    | Business condition |
| Role dependency    | Yes               | No                 |
| Hierarchy required | No                | No                 |

---

## ⚠️ Common Interview Traps

### ❌ Sharing rule se access kam karna

Impossible

---

### ❌ Sharing rule admin ke liye

Admins already have access

---

### ❌ Profile se sharing rule control

Profiles ka koi role nahi

---

## 🏢 Real Project Example (Insurance)

### Object: Policy__c

### OWD: Private

### Rules:

1️⃣ Owner-based:

* Owner role = Agent
* Share with Manager (Read)

2️⃣ Criteria-based:

* Policy_Type = “Corporate”
* Share with Corporate Team (RW)

➡️ Clean multi-dimensional sharing

---

## 📝 Interview-Ready Answer (Power)

> “Owner-based sharing rules provide access based on the record owner’s role or group, while criteria-based sharing rules share records dynamically based on field values. Both are used to extend access beyond restrictive OWD and cannot reduce existing access.”

---

## 🧠 Memory Trick

> - **Owner-based = WHO owns it 👤**
> - **Criteria-based = WHAT the record is 🏷️**

---
---
---
---

# 🔐 Manual Sharing – Deep Dive (Salesforce)

**Manual Sharing** ka matlab:

> 👉 **Ek specific record ko manually kisi user / role / group ke saath share karna**

- 📌 Ye **automatic nahi hota**
- 📌 Ye **record-by-record** hota hai
- 📌 Ye **temporary / exception-based access** ke liye hota hai

Ye feature **Salesforce** me tab use hota hai jab rules kaafi nahi hote.

---

## 🧠 Manual Sharing kab kaam karta hai?

Manual Sharing **sirf tab effective hota hai** jab:

* OWD = **Private**
* ya **Public Read Only**

❌ OWD = Public Read/Write → Manual sharing ka koi meaning nahi

---

## 👤 Kaun manually share kar sakta hai?

Sirf ye log:

| Who                                | Reason             |
| ---------------------------------- | ------------------ |
| Record Owner                       | Natural owner      |
| System Administrator               | God mode           |
| User with **Modify All**           | Full control       |
| User with **Modify All on object** | Object-level power |

📌 Normal user **dusre ka record share nahi kar sakta**

---

## 🎯 Manual Sharing kya control karta hai?

Sirf **record access level**:

| Access Level | Meaning            |
| ------------ | ------------------ |
| Read         | Record dekh sakta  |
| Read/Write   | Edit bhi kar sakta |

❌ Delete kabhi manual sharing se nahi milta

---

## 📍 Manual Sharing UI kaha hoti hai?

Classic / Lightning me:

* Record open karo
* **Sharing** button / section
* User / Role / Public Group select karo
* Access level choose karo

---

## 🧩 Simple Example

### Scenario:

* Object: Account
* OWD = Private

User A owns Account A1
User B ko temporary access chahiye

### Action:

* A1 → Share with User B → Read

➡️ User B ab A1 dekh sakta hai

---

## 🔥 Tricky Interview & Project Edge Cases

### 🔥 Case 1: Owner change ho gaya

❓ Kya manual sharing rahegi?

👉 **YES**, but:

* Agar sharing **old owner ne di thi**
* Salesforce usko **remove kar deta hai**

📌 Owner-based recalculation hota hai

---

### 🔥 Case 2: Record delete / undelete

* Delete → sharing gone
* Undelete → sharing **restore hoti hai**

📌 Salesforce restore kar deta hai

---

### 🔥 Case 3: Role hierarchy ka effect

* Manager ko already access role se mil raha
* Manual sharing add kar di

👉 **No change** (duplicate access ignore)

📌 Highest access wins

---

### 🔥 Case 4: Field / Object access missing

❓ Record share ho gaya, fir bhi user record nahi dekh pa raha?

👉 Reason:

* Object Read permission ❌
* Field Level Security ❌

📌 Manual sharing **sirf record level** pe kaam karta hai

---

### 🔥 Case 5: Manual sharing vs Sharing Rule

| Point       | Manual | Sharing Rule |
| ----------- | ------ | ------------ |
| Automation  | ❌      | ✅            |
| Scale       | Low    | High         |
| Temporary   | ✅      | ❌            |
| Performance | Light  | Heavy        |

---

### 🔥 Case 6: Manual sharing & Custom Object (Hierarchy OFF)

* Custom object
* Grant Access Using Hierarchies = OFF

👉 Manual sharing **still works perfectly**

📌 Completely independent

---

## 🏢 Real Project Use Cases

### 🏦 Banking

* Auditor ko **specific customer record** temporarily dikhaana
* Manual sharing best option

---

### 🏥 Healthcare

* Doctor ko ek patient ka record temporarily share
* After treatment → remove sharing

---

### 🏢 Corporate

* Manager on leave → delegate record to colleague

---

## ⚠️ Common Mistakes (Interview Gold)

❌ Manual sharing ko permanent solution banana
❌ Thousands of records manually share karna
❌ Object access diye bina sharing expect karna

---

## 📝 Interview-Ready Definition

> **Manual Sharing in Salesforce allows record owners or administrators to manually grant read or read/write access to specific records for selected users, roles, or public groups. It is primarily used for temporary or exception-based access scenarios.**

---

## 🧠 Memory Trick

> **OWD = Lock 🔒**
> **Sharing Rule = Auto key 🔑**
> **Manual Sharing = Spare key (temporary) 🗝️**

---



