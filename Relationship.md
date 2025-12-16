# Salesforce Relationships – Interview Questions

---

## 1. What is a Relationship in Salesforce?

**Answer:**
Salesforce me relationship ka matlab hai **do ya zyada objects ko connect karna** taaki related data ko easily store, access aur manage kiya ja sake.
Real-time projects me relationships data integrity, reporting, automation aur security ke liye bahut important hoti hain.

---

## 2. What are the different types of relationships in Salesforce?

**Answer:**
Salesforce me mainly ye relationships hoti hain:

* Lookup Relationship
* Master-Detail Relationship
* Many-to-Many Relationship
* Hierarchical Relationship
* Self Relationship
* External Lookup Relationship

---

## 3. Difference between Lookup Relationship and Master-Detail Relationship?

**Answer:**

| Feature              | Lookup Relationship | Master-Detail Relationship |
| -------------------- | ------------------- | -------------------------- |
| Connection Type      | Loose               | Strong                     |
| Cascade Delete       | ❌ No                | ✅ Yes                      |
| Owner Field on Child | ✅ Yes               | ❌ No                       |
| Roll-Up Summary      | ❌ No                | ✅ Yes                      |
| Reparenting          | Always allowed      | Optional                   |
| Security             | Independent         | Inherits from parent       |

---

## 4. When would you prefer Master-Detail over Lookup?

**Answer:**
Jab child record ka existence parent ke bina possible na ho, ownership aur security parent se inherit karni ho, aur roll-up summary chahiye ho, tab Master-Detail relationship use karte hain.

---

## 5. Can we convert Lookup Relationship into Master-Detail?

**Answer:**
Haan, lekin kuch conditions ke saath:

* Child object ke saare records me parent value populated honi chahiye
* Child object me **Owner field** nahi hona chahiye
* Sharing model compatible hona chahiye
* Agar conditions meet na ho to Salesforce conversion allow nahi karta

---

## 6. Can we convert Master-Detail into Lookup?

**Answer:**
Haan, possible hai.
Isme ownership aur sharing child object par independent ho jaati hai aur roll-up summary fields ko remove karna padta hai.

---

## 7. What is Roll-Up Summary and where is it used?

**Answer:**
Roll-Up Summary ek special field hota hai jo child records ka summary data parent record par show karta hai.
Ye sirf Master-Detail Relationship ke case me aur sirf parent object par available hota hai.

---

## 8. What types of fields can be used in Roll-Up Summary?

**Answer:**
Sirf numerical aur date-based fields:

* Number
* Currency
* Percentage
* Date
* DateTime

---

## 9. What is Data Skew and how do you handle it?

**Answer:**
Data skew ek performance issue hai jo tab hota hai jab ek parent record ke under 10,000+ child records ho jaate hain.
Isko handle karne ke liye:

* Parent records ko distribute karte hain
* Lookup relationship use karte hain jahan possible ho
* Large data volumes ke liye async processing use karte hain

---

## 10. How many relationships can an object have?

**Answer:**

* Maximum 40 Lookup Relationships
* Maximum 2 Master-Detail Relationships
* Maximum 40 Roll-Up Summary fields

---

## 11. What is a Many-to-Many Relationship and how is it implemented?

**Answer:**
Many-to-Many relationship tab use hoti hai jab ek object ke multiple records dusre object ke multiple records se connect hote hain.
Isko implement karte hain:

* Junction Object ke through
* Junction object me dono parents ke saath Master-Detail relationship hoti hai

---

## 12. Can a standard object be a detail in Master-Detail relationship?

**Answer:**
Nahi.
Agar master side par custom object hai, to standard object detail side par nahi ho sakta.

---

## 13. Can Lead or User be a Master in Master-Detail relationship?

**Answer:**
Nahi.
Salesforce Lead aur User objects ko master side par allow nahi karta.

---

## 14. What is Reparenting in Master-Detail?

**Answer:**
Reparenting ka matlab hai child record ko ek master record se dusre master record me move karna.
By default ye disabled hota hai aur relationship create karte time “Allow Reparenting” enable karna padta hai.

---

## 15. How do you identify relationship types using Schema Builder?

**Answer:**
Schema Builder me:

* Line / thread ke color aur structure se relationship type identify hota hai
* Three lines wali side child hoti hai
* One line wali side parent hoti hai

---

## 16. What is the relationship between Account and Contact?

**Answer:**
By default Account aur Contact ke beech Lookup relationship hota hai, lekin Salesforce internally isko Master-Detail jaisa treat karta hai, jahan Account delete hone par Contact bhi delete ho jaate hain.

---

## 17. Can Roll-Up Summary work with Lookup Relationship?

**Answer:**
Nahi.
Roll-Up Summary sirf Master-Detail Relationship ke saath kaam karta hai.
Lookup ke case me workaround ke liye Flow, Trigger, ya Declarative Roll-Up tools use karte hain.

---

## 18. How do you handle roll-up summary when relationship is Lookup?

**Answer:**

* Record-triggered Flow
* Apex Trigger
* Declarative Roll-Up Summary (DLRS) tool

---

## 19. What happens to child records when master record is restored from recycle bin?

**Answer:**
Master restore hote hi uske saare child records bhi automatically restore ho jaate hain.

---

## 20. Real Project Scenario Question

**Question:**
Student aur Course ke beech relationship kaunsa hoga?

**Answer:**
Many-to-Many relationship, implemented using a Junction Object with two Master-Detail relationships.

---

# Salesforce Relationships – Tricky Interview Trap Questions

## 1. Can we create Roll-Up Summary on a Lookup Relationship?

**Answer:**
❌ No, Roll-Up Summary sirf **Master-Detail Relationship** me possible hota hai.

**Trap Point:**
Interview me bolte hain *“can we summarize child data in lookup?”*
Correct approach: **Flow / Apex / DLRS** ka use karna padta hai.

---

## 2. If we delete a Master record, where do the child records go?

**Answer:**
Child records **recycle bin me visible nahi hote**, lekin backend me stored rehte hain.

**Important Detail:**
Master restore karte hi saare child records bhi automatically restore ho jaate hain.

---

## 3. Can a child record in Master-Detail have its own owner?

**Answer:**
❌ No.

**Explanation:**
Child record owner inherit karta hai master se, isliye **Owner field child me hota hi nahi**.

---

## 4. Can we have more than 2 Master-Detail Relationships on a single object?

**Answer:**
❌ No.

**Limit:**

* Max **2 MDR**
* Max **40 Lookup Relationships**

---

## 5. Can a standard object be on the detail side in Master-Detail?

**Answer:**
❌ No, jab master side par custom object ho.

**Trap:**
Ye rule sirf **Master = Custom & Detail = Standard** ke case me fail hota hai.

---

## 6. Is it possible to convert a Lookup Relationship into Master-Detail?

**Answer:**
✅ Yes, but with conditions.

**Conditions:**

* Child records me parent value blank nahi hona chahiye
* Child object me Owner field hona allowed nahi
* Sharing model compatible hona chahiye

---

## 7. Is reparenting always available in Master-Detail?

**Answer:**
❌ No.

**Explanation:**
Reparenting sirf tab possible hai jab relationship create karte time **“Allow Reparenting”** enable kiya ho.

---

## 8. Can we create Roll-Up Summary on child object?

**Answer:**
❌ No.

**Correct Rule:**
Roll-Up Summary **sirf parent (master) object** par create hota hai.

---

## 9. What happens if a Master record has more than 10,000 child records?

**Answer:**
Performance issue aata hai jise **Data Skew** kehte hain.

**Impact:**

* Sharing slow
* Reports slow
* DML operations slow

---

## 10. Can Lead or User be a Master in Master-Detail?

**Answer:**
❌ No.

**Trap:**
Interview me log bol dete hain “standard object ho sakta hai”, but **Lead aur User exception hain**.

---

## 11. Account–Contact relationship Lookup hai ya Master-Detail?

**Answer:**
By default **Lookup** hota hai,
lekin behavior **Master-Detail jaisa** hota hai.

**Reason:**
Salesforce internally cascade delete manage karta hai.

---

## 12. Can we create Roll-Up Summary if Master-Detail relationship is indirect?

**Answer:**
❌ No.

**Explanation:**
Roll-Up Summary sirf **direct MDR** par kaam karta hai.

---

## 13. How do you identify MDR vs LR in Schema Builder?

**Answer:**

* **Three lines** → Child side
* **One line** → Parent side
* Thread color se bhi differentiate hota hai

---

## 14. Can we make a Lookup field mandatory?

**Answer:**
✅ Yes.

**Trap:**
Mandatory hone se bhi Lookup **strong relationship** nahi ban jaata.
Cascade delete aur ownership phir bhi apply nahi hoti.

---

## 15. Can a child record exist without parent in Master-Detail?

**Answer:**
❌ No.

**Reason:**
MDR me child ka existence parent par fully dependent hota hai.

---

# Scenario-Based Salesforce Relationship Questions (Real Project Level)

---

## 1. Student–Course Relationship ka design kaise karoge?

**Scenario:**
Ek student multiple courses le sakta hai aur ek course me multiple students ho sakte hain.

**Answer:**
Ye **Many-to-Many relationship** hai.
Isko **Junction Object** ke through implement karenge jisme:

* Student → Master-Detail
* Course → Master-Detail

**Reason:**
Dono sides par multiple records ho sakte hain aur junction object future me extra fields (grade, enrollment date) bhi store kar sakta hai.

---

## 2. Order aur Order Items ke beech kaunsa relationship use karoge?

**Answer:**
**Master-Detail Relationship**

**Reason:**

* Order delete hone par Order Items ka koi meaning nahi
* Roll-up summary chahiye (Total Amount)
* Ownership aur sharing parent se inherit honi chahiye

---

## 3. Account aur Case ke beech kaunsa relationship prefer karoge?

**Answer:**
**Lookup Relationship**

**Reason:**

* Case independently exist kar sakta hai
* Case ka owner Account se different ho sakta hai
* Deleting Account should not always delete Cases (business dependent)

---

## 4. Lookup vs Master-Detail ka decision kaise loge?

**Answer:**
Main ye check karta hoon:

* Kya child record parent ke bina exist kar sakta hai?
* Kya cascade delete chahiye?
* Kya roll-up summary required hai?
* Kya ownership inherit honi chahiye?

Agar inme se zyada answers “yes” hain → **Master-Detail**, warna **Lookup**.

---

## 5. Lookup relationship me Roll-Up Summary chahiye, kya karoge?

**Answer:**
Lookup me direct Roll-Up Summary possible nahi hai.
Solution:

* Record-Triggered Flow (preferred)
* Apex Trigger (agar complex logic ho)
* DLRS tool (agar allowed ho)

---

## 6. Ek parent record ke under 50k child records aa rahe hain, issue kya hoga?

**Answer:**
Ye **Data Skew** create karega.

**Handling:**

* Parent records ko distribute karna
* Lookup relationship use karna jahan possible ho
* Async processing (Batch / Queueable)

---

## 7. Invoice delete hone par Payments bhi delete ho jaye, kaunsa relationship?

**Answer:**
**Master-Detail Relationship**

**Reason:**
Payments ka existence Invoice ke bina nahi hona chahiye aur cascade delete required hai.

---

## 8. Product aur Price Book Entry ke beech relationship kaunsa hota hai?

**Answer:**
Lookup Relationship

**Reason:**
Price Book Entry independently manage hoti hai aur standard Salesforce design follow karta hai.

---

## 9. Employee aur Manager relationship kaise design karoge?

**Answer:**
**Self Relationship**

**Reason:**
Employee object khud se hi related hota hai (Manager bhi ek employee hai).

---

## 10. Hierarchical Relationship kab use hoti hai?

**Answer:**
Sirf **User object** ke liye.

**Example:**
Manager → Subordinate hierarchy for approvals and reporting.

---

## 11. Existing Lookup ko Master-Detail me convert karna ho, approach?

**Answer:**
Steps:

* Ensure parent field is populated for all child records
* Remove Owner field dependency
* Check sharing model
* Then convert Lookup to Master-Detail

---

## 12. Reporting ke liye strong data integrity chahiye, kaunsa relationship?

**Answer:**
**Master-Detail Relationship**

**Reason:**
Roll-up summary, consistent sharing, aur cascade delete reporting ko reliable banata hai.

---

## 13. External system (SAP / DB table) ke saath relationship kaise banate ho?

**Answer:**
**External Lookup Relationship**

**Reason:**
Salesforce objects ko external objects se link karna hota hai without copying data.

---

## 14. Child record ko dusre parent ke under move karna ho, kaunsa feature?

**Answer:**
**Reparenting (MDR)**

**Condition:**
“Allow Reparenting” enabled hona chahiye.

---

## 15. Account delete hone par Contacts delete nahi hone chahiye, design?

**Answer:**
**Lookup Relationship** (custom scenario)

**Note:**
Standard Account–Contact Salesforce internally MDR jaisa behave karta hai, lekin custom design me lookup prefer karenge.

---

## 16. Security strictly parent ke according honi chahiye, kaunsa relationship?

**Answer:**
**Master-Detail Relationship**

**Reason:**
Child automatically parent ki sharing follow karta hai.

---

## 17. Junction Object kab avoid karoge?

**Answer:**
Jab:

* Extra fields ki need na ho
* Simple lookup sufficient ho
* Performance concern ho

---

## 18. Schema Builder kab use karte ho in projects?

**Answer:**

* Object relationships visualize karne ke liye
* Quick validation ke liye
* Interview me explanation ke liye 😄

---

# Advanced Edge-Case Salesforce Relationship Scenarios

---

## 1. Roll-Up Summary chahiye but relationship Lookup hai aur data volume bahut zyada hai

**Scenario:**
Parent ke under 100k+ child records hain, Lookup relationship hai, aur real-time roll-up required hai.

**Answer / Approach:**

* Direct Roll-Up Summary possible nahi
* **Record-Triggered Flow** avoid karunga (performance issue)
* **Apex Trigger + Async processing (Queueable / Batch)** use karunga
* Incremental updates karunga instead of full recalculation

**Why:**
Flows large volumes me governor limits hit kar sakte hain.

---

## 2. Child record mandatory hona chahiye but cascade delete nahi chahiye

**Scenario:**
Parent ke bina child exist nahi kare, lekin parent delete hone par child delete nahi hona chahiye.

**Answer:**

* **Lookup Relationship** use karunga
* Lookup field ko **required** banaunga
* Delete protection ke liye **Validation Rule / Flow** lagaunga

**Reason:**
MDR me cascade delete unavoidable hota hai.

---

## 3. Parent delete hone par kuch child records delete ho aur kuch survive kare

**Scenario:**
Partial cascade delete chahiye.

**Answer:**

* **Lookup Relationship** use karunga
* Custom delete logic likhunga (Flow / Trigger)
* Business rule ke basis par selective delete karunga

**Reason:**
MDR me selective behavior possible nahi.

---

## 4. Data skew aa raha hai but roll-up summary bhi chahiye

**Scenario:**
Ek master record ke under 20k+ child records hain aur performance degrade ho rahi hai.

**Answer:**

* Parent records ko **logical partition** karunga
* Junction object introduce karunga
* Direct MDR avoid karunga jahan possible ho

**Why:**
Single parent pe zyada child records Salesforce ke sharing engine ko slow kar dete hain.

---

## 5. Security child record pe alag honi chahiye but roll-up bhi chahiye

**Scenario:**
Child ki sharing independent ho, par parent ko summary bhi dikhe.

**Answer:**

* **Lookup Relationship** maintain karunga
* Roll-up ke liye Flow / Apex use karunga

**Reason:**
MDR me child ki security parent se forced hoti hai.

---

## 6. Existing MDR ko Lookup me convert karna hai but roll-up summaries already hain

**Scenario:**
Production org, active roll-ups exist karte hain.

**Answer:**

* Pehle roll-up fields ko remove / replace karunga
* Custom roll-up logic implement karunga
* Phir MDR → Lookup conversion karunga

**Why:**
Roll-up summary Lookup me supported nahi hai.

---

## 7. Junction Object me ek relationship optional aur ek mandatory chahiye

**Scenario:**
Many-to-Many hai, lekin ek side optional hai.

**Answer:**

* Mandatory side → Master-Detail
* Optional side → Lookup

**Reason:**
Salesforce allow karta hai hybrid design in junction objects.

---

## 8. Parent object standard hai aur usme roll-up chahiye but child custom hai

**Scenario:**
Standard object me Roll-Up Summary field option disabled dikh raha hai.

**Answer:**

* Check karunga relationship **direct MDR** hai ya nahi
* Agar standard object limitation hai to Flow / Apex use karunga

---

## 9. Reparenting chahiye but data integrity break nahi honi chahiye

**Scenario:**
Child record ko parent change karna hai but business rules strict hain.

**Answer:**

* Reparenting enable karunga
* Validation Rules lagaunga
* Before-update checks karunga

---

## 10. Parent restore hone par child restore nahi hone chahiye

**Scenario:**
Delete ke baad selective restore required hai.

**Answer:**

* **MDR avoid karunga**
* Lookup + custom restore logic use karunga

**Reason:**
MDR me restore behavior automatic hota hai.

---

## 11. Reporting slow ho rahi hai due to deep relationships

**Scenario:**
Multiple object joins ke wajah se reports slow hain.

**Answer:**

* Relationship depth reduce karunga
* Summary objects introduce karunga
* Flattened reporting design banaunga

---

## 12. External system data ko Salesforce se tightly link karna hai

**Scenario:**
External DB records ko Salesforce ke delete ke saath control nahi kar sakte.

**Answer:**

* **External Lookup Relationship** use karunga
* Cascade delete expectations clear karunga (not supported)

---

## 13. Child object ko future me independently use karna ho sakta hai

**Scenario:**
Aaj dependency strong hai, future unclear.

**Answer:**

* Initially **Lookup Relationship** choose karunga
* Business mature hone par MDR evaluate karunga

---

## 14. Salesforce limit hit ho rahi hai relationships ki

**Scenario:**
Object already 40 lookups use kar raha hai.

**Answer:**

* Relationship audit karunga
* Unused lookups remove karunga
* Junction / polymorphic design explore karunga

---

## 15. Interview Trap Edge Case

**Question:**
“Can we fully replace Master-Detail with Lookup + Flow?”

**Answer:**
Technically possible, **but not recommended** for:

* Ownership inheritance
* Security model
* Platform-level optimizations

---

# 🔥 Tricky Interview Questions – Master-Detail with Existing Data

---

### 1️⃣ **Why Salesforce does not allow direct Master-Detail creation when child object already has records?**

**Expected Answer:**

Salesforce **data integrity** maintain karta hai.
Master-Detail me **child record ka parent mandatory hota hai**.

Agar child object me existing records hain aur unka parent undefined hai, to:

* Orphan records ban sakte hain
* Roll-up summary, sharing, cascade delete break ho sakta hai

Isliye Salesforce **direct MDR creation block kar deta hai**.

---

### 2️⃣ **Can we force Master-Detail creation by making the field required?**

❌ **No**

**Reason:**

* Field required karna **future records** ke liye hota hai
* Existing records fir bhi **parent-less** rahenge
* Salesforce existing data ko auto-assign nahi karta

👉 Isliye Lookup → Data Update → Convert is the only safe path.

---

### 3️⃣ **Why Lookup Relationship is allowed but Master-Detail is not?**

**Answer:**

| Lookup            | Master-Detail            |
| ----------------- | ------------------------ |
| Parent optional   | Parent mandatory         |
| Child independent | Child dependent          |
| No cascade delete | Cascade delete           |
| Own sharing       | Parent sharing inherited |

Lookup **flexible hoti hai**, isliye existing data ke saath safe hoti hai.

---

### 4️⃣ **What will happen if even one child record has blank parent during conversion?**

🔥 **Conversion FAIL ho jayega**

Salesforce error dega:

> “Cannot convert lookup to master-detail because some records do not have a parent.”

👉 **All child records must have parent populated** — even 1 blank record is blocker.

---

### 5️⃣ **Can we use Data Loader to solve this problem? How?**

✅ **Yes (Best practice in large data)**

**Steps:**

1. Export child records where parent lookup is blank
2. Identify correct parent record IDs
3. Update child records using Data Loader
4. Re-attempt conversion to Master-Detail

📌 Real projects me ye approach most common hai.

---

### 6️⃣ **What happens to sharing settings after Lookup → Master-Detail conversion?**

⚠️ **Important trap question**

**Answer:**

* Child object ka **sharing model automatically removed**
* Child records **parent ke sharing rules inherit karte hain**
* Manual sharing on child **no longer works**

👉 Interviewers often check if you know this impact.

---

### 7️⃣ **Will existing roll-up summary fields work after conversion?**

❌ **No**

**Reason:**

* Roll-up summary fields **sirf Master-Detail par work karte hain**
* Lookup relationship me allowed nahi hote

👉 Conversion ke baad:

* You can **create new roll-up summary fields**
* Old formula/workaround logic replace ho jata hai

---

### 8️⃣ **Can we convert Master-Detail back to Lookup later? Any risks?**

⚠️ **Yes, but risky**

**Risks:**

* Roll-up summary fields will be deleted
* Child sharing model must be re-defined
* Cascade delete behavior removed

👉 Production me convert back karne se pehle **full impact analysis** zaroori hai.

---

### 9️⃣ **Is it possible to have validation rule blocking conversion even if data looks correct?**

✅ **Yes**

**Examples:**

* Validation rule requiring parent based on condition
* Trigger blocking update on child records
* Required fields on parent not satisfied

👉 Interview tip:
“Always check validation rules & triggers before conversion.”

---

### 🔟 **Real-World Project Question (Very Tricky)**

**Question:**

> You have 1 million child records. How will you safely convert Lookup to Master-Detail?

**Strong Answer:**

* Create Lookup first
* Use **batch update / Data Loader** to populate parent
* Validate using SOQL (no null parent)
* Test conversion in **full sandbox**
* Convert during **low-traffic deployment window**

📌 This shows **architect-level thinking**.

---

## ⭐ One-Line Smart Interview Closing

> “For existing data, Salesforce enforces a Lookup-first approach to ensure data integrity before allowing Master-Detail dependency.”

---


Perfect 👍
Neeche **Salesforce Many-to-Many Relationship** par based **TRICKY + REAL PROJECT LEVEL interview questions** diye gaye hain — **6+ years experience** ke hisaab se, **Hinglish**, aur **interviewer-trap focused**.

---

## 🔗 Many-to-Many Relationship – Quick Recall (1 Line)

> Salesforce me Many-to-Many relationship **direct possible nahi hoti**, iske liye **Junction Object** use hota hai jisme **2 Master-Detail relationships** hoti hain.

---

# 🔥 Tricky Interview Questions – Many-to-Many (Advanced)

---

### 1️⃣ **Why Salesforce does not support direct Many-to-Many relationships?**

**Answer:**

Salesforce ka relational model **strict data ownership & sharing rules** follow karta hai.
Direct many-to-many me:

* Ownership ambiguity hoti hai
* Sharing & security unclear ho jati hai
* Roll-up & cascade behavior unpredictable ho jata hai

Isliye Salesforce **Junction Object approach enforce karta hai**.

---

### 2️⃣ **Can a Junction Object have Lookup instead of Master-Detail?**

⚠️ **Trap Question**

**Answer:**
❌ **Not recommended**

Technically possible hai, but:

* Roll-up summary fields ka benefit nahi milega
* Cascade delete ka control nahi milega
* Data integrity weak ho jati hai

👉 **Best Practice:**
Junction Object = **2 Master-Detail relationships**

---

### 3️⃣ **Which master controls ownership in a Junction Object?**

🔥 **Very common trap**

**Answer:**

* Junction Object ka **ownership first Master-Detail relationship** se aata hai
* Second master sirf relationship maintain karta hai
* You **cannot have independent owner** on junction object

📌 Interview Tip:
Order of Master-Detail creation **matters**.

---

### 4️⃣ **What happens if you delete one master record?**

**Answer:**

* Us master se linked **junction records automatically deleted**
* Second master record **safe rehta hai**

Example:

* Student ↔ Course
* Student delete → Enrollment (junction) delete
* Course remains

---

### 5️⃣ **Can we create Roll-Up Summary fields in Many-to-Many?**

✅ **Yes, but condition ke saath**

**Answer:**

* Roll-up summary **sirf Master object par**
* Junction object ke fields ka aggregation hota hai

Example:

* Account ← AccountContactRelation (junction)
* Account par contacts ka count / sum possible

---

### 6️⃣ **Can a Junction Object have its own fields?**

✅ **Yes (and very important)**

**Answer:**
Junction object sirf relationship ke liye nahi hota, usme:

* Status
* Start Date
* Role
* Quantity
  jaise **business-specific fields hote hain**

📌 Real Project Example:

> Opportunity ↔ Product → OpportunityLineItem

---

### 7️⃣ **Is it mandatory that both relationships in Junction Object are Master-Detail?**

⚠️ **Advanced Trap**

**Answer:**

❌ **No (technically)**
But ✅ **Yes (practically & best practice)**

Agar:

* Ek Master-Detail + Ek Lookup → possible hai
* But sharing, roll-up & delete behavior complex ho jata hai

👉 Salesforce recommends **2 Master-Detail only**

---

### 8️⃣ **What happens to sharing rules in Many-to-Many?**

**Answer:**

* Junction object ka sharing **primary master se inherit hota hai**
* Secondary master ka sharing ignored hota hai
* Manual sharing not allowed on junction object

🔥 Interviewers yahin confuse karte hain.

---

### 9️⃣ **Can we convert Lookup-based Junction to Master-Detail later?**

✅ **Yes, but risky**

**Steps:**

1. Ensure all junction records have both parent references
2. Check validation rules & triggers
3. Convert Lookup → Master-Detail
4. Re-test roll-ups & sharing

⚠️ Production me bina testing **never convert**.

---

### 🔟 **Real-World Scenario Question (Architect Level)**

**Question:**

> One Product can belong to multiple Opportunities, and one Opportunity can have multiple Products. How will you design this?

**Strong Answer:**

* Create **OpportunityLineItem (Junction Object)**
* 2 Master-Detail relationships:

  * Opportunity → OLI
  * Product → OLI
* Quantity, Price, Discount as fields on junction

📌 This is **classic Salesforce many-to-many**.

---

### 1️⃣1️⃣ **Can we build Many-to-Many without Junction Object using automation?**

❌ **No (Trap)**

Automation (Flow/Trigger) **relationship replace nahi kar sakta**
Data duplication hogi
Referential integrity break hogi

👉 Junction object is **mandatory**

---

### 1️⃣2️⃣ **What is the biggest risk in Many-to-Many design?**

**Answer:**

* Wrong master order
* Unexpected cascade delete
* Sharing visibility issues
* Performance issues due to large junction volume

📌 Senior devs pehle **delete impact analysis** karte hain.

---

## ⭐ Smart Interview One-Liner

> “In Salesforce, a Many-to-Many relationship is implemented using a junction object with two master-detail relationships, where the primary master controls ownership, sharing, and security.”

---
