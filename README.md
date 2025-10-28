# Salesforce Admin

## Table of Contents

1. [Field History Tracking](#field-history-tracking)
2. [Field Deletion Considerations](#field-deletion-considerations)
3. [Global Picklist](#global-picklist)
4. [Field Dependency](#field-dependency)
5. 

## Salesforce Basic
- Salesforce Classic Experience (CEX)
- Salesforce Lightning Experience (LEX)
- 9 dots - App Launcher
- Department = Profile
- Database table = Objects
- Dropdown list = Picklist

Important for job :<br/>
If anything we get by default in Salesforce software = "Standard"<br/>
If anything we create in Salesforce software by our own efforts = "Custom"

<b>Q. What is the new field in Salesforce that you worked ? (Tesla Motors, USA)</b><br/>
A. Time


---
---
---
---

## Field History Tracking

Field History Tracking allows Salesforce users to monitor changes to specific fields on records, helping in audit, troubleshooting, and data integrity analysis.

### 1. Benefits of Field Tracking

**Q:** What are the benefits of field tracking in your job?<br/>**A:**

* Helps identify **who changed what and when**.
* Useful for **auditing** and maintaining **data accuracy**.
* Supports **compliance** and **debugging** by providing a history of field changes.
* Enables better **user accountability** and **data governance**.

### 2. Tracking Standard Fields

**Q:** Can we track standard fields? *(TCS)*<br/>
**A:**
Yes — but only **two** standard fields can be tracked:

* **Owner**
* **Name (Auto Number)**

### 3. Standard Fields That Cannot Be Tracked

**Q:** Which standard fields cannot be tracked, and why?
<br/>
**A:**

* **CreatedBy** and **LastModifiedBy** cannot be tracked.

**Reasons:**

1. **CreatedBy** – Record creation happens only once, so Salesforce does not provide tracking for this field.
2. **LastModifiedBy** – This field updates frequently, and tracking it would not add meaningful insights since it changes with every edit. Also, it doesn’t specify **which fields** were changed.


### 4. Reliability of "Last Modified By"

**Q:** What issues arise when relying on "Last Modified By" for tracking data changes? *(IBM)*<br/>
**A:**

* It only shows **who modified** the record, **not which fields** were changed.
* Therefore, it is **not a reliable source** for detailed change tracking.

### 5. When Field Tracking Details Are Missing

**Q:** If a user cannot see field tracking details in the related section, what should you do?<br/>
**OR**<br/>
**Q:** What are the reasons field changes might not be tracked?<br/>
**A:**<br/>
Possible reasons include:

1. **Field History Tracking** not enabled for that object.
2. Specific fields were **not selected** for tracking.
3. Field type is **unsupported** for tracking (e.g., Formula or Long Text fields).
4. **User profile permissions** or **field-level security** settings prevent visibility.
5. Field tracking history is **older than the retention limit** and has been purged.


### 6. Data vs. Settings Tracking

**Q:** Field tracking helps us to see only “xxx changes,” not “yyy changes.”<br/>
**A:**

* **xxx = Data changes**
* **yyy = Settings changes**

*Field tracking only records changes to data values, not configuration or metadata changes.*

### 7. Fields That Are Not Fully Tracked

**Q:** History tracking shows “Changed [Field Name]” instead of old/new values for some fields. Which fields are those?<br/>
**A:**
Field tracking does **not** record old and new values for:

* **Formula Fields**
* **Encrypted Fields**
* **Rich Text Areas**
* **Long Text Areas**
* **Multi-select Picklists**
* Fields with **more than 255 characters**

### 8. Fields Ineligible for Tracking

**Q:** For which custom fields (below 255 length) can we not enable field tracking? *(Infosys)*<br/>
**A:**

* **Formula Fields**
* **Auto Number Fields**
* **Roll-Up Summary Fields**

### 9. Data Retention

**Q:** How long can we retain data in the Field History Tracking table? *(Disney)*<br/>
**A:**

* **Without coding:** Up to **18 months**
* **With coding (via API or export):** Up to **24 months**

> **Note:** Field History Tracking data does **not count** against your Salesforce org’s **data storage limits**.


### 10. Field Tracking Limit

**Q:** How many fields can we track per object? *(Chase Bank)*<br/>
**A:**
* You can track **up to 20 fields per object**.

---
---
---
---

## Field Deletion consideration 
Here’s a clean, professional, and well-organized version of your documentation text — formatted for clarity and usability:


### Recycle Bin: Records vs. Fields

### 1. Difference

* **Records**: When a record is deleted, it is moved to the **Recycle Bin**.
* **Fields**: When a field is deleted, it appears under the **Deleted Fields** section within **Fields & Relationships** on the object.

### 2. Commonality

* Both deleted **records** and **fields** remain recoverable for **15 days**.
* After **15 days**, they are **permanently deleted** and cannot be restored.

### Additional Notes

* If you want to **free up storage space**, you must **permanently delete** the fields.

  * Simply deleting a field (without permanent deletion) does **not** free up space.
  * **Best Practice:** Permanently delete unused fields when you no longer need them.
* You can check **field limitations and usage** by navigating to:
  **Setup → Object Manager → [Object Name] → Object Limits**

### Field Recovery Behavior

### Q. After undeleting fields, are the field values recovered?

**A.** Yes — when a field is undeleted, all its previous **values** are **restored**.

### Additional Details

* Once a field is deleted:
  * It no longer appears on the **detail page**.
  * It is also removed from the **field history tracking** section.
* When a deleted field is recovered:
  * Its **data** and **history** are restored.

#### Recovery Limitations

| Deleted Item | Recoverable? |
| ------------ | ------------ |
| Object       | ✅ Yes        |
| Field        | ✅ Yes        |
| App          | ❌ No         |

### Important Rules for Field Deletion and Recovery

When fields are **deleted and later recovered**, certain properties and behaviors may not be fully restored. Below are key considerations and corrective actions:

#### 1. Unique Fields

* **Behavior:**

  * A field created with the **Text** data type and marked as **Unique** will function correctly as long as it remains active.
  * However, if this field is **deleted** and later **recovered**, it **loses its uniqueness property**.
* **Action Required:**

  * Manually re-enable the **Unique** attribute after recovery if uniqueness is required.


#### 2. Required Fields

* **Behavior:**

  * A field marked as **Required** works normally during record creation.
  * If this field is **deleted** and later **recovered**, it **loses both its visibility and required properties**.
  * The field will not be visible on the page after recovery.
* **Action Required:**

  1. Go to **Set Field-Level Security** and re-enable visibility for the appropriate profiles.
  2. Open the **Edit Field** section and re-select the **Required** checkbox.


#### 3. Custom Fields and Page Layouts

* **Behavior:**

  * A **custom field** will function normally until deleted.
  * If it is **deleted**, and the **page layout** is modified while it is in the deleted state, then upon recovery, the field may **not automatically appear** on the page layout.
* **Action Required:**

  * Navigate to **Page Layouts** and **manually drag and drop** the recovered field into the desired section.

#### Summary

| Scenario                      | Issue After Recovery         | Action to Fix                                    |
| ----------------------------- | ---------------------------- | ------------------------------------------------ |
| Unique Field                  | Uniqueness removed           | Re-enable “Unique” property                      |
| Required Field                | Not visible and not required | Re-set field-level security and mark as required |
| Custom Field (Layout Changed) | Not visible on page layout   | Add manually to page layout                      |

---
---
---
---

## Global Picklist
A Global Picklist (also known as a Global Value Set or Picklist Value Set) is a reusable list of picklist values that can be shared across multiple objects and fields within Salesforce.
This helps maintain consistency, data integrity, and easier maintenance when the same set of options is used in multiple places.

How to decide when we need to create a local or a global PL?</br>
- Becoming proactive in ur project</br>
- Check requirement doc neatly</br>
- Asking BA

<b>Q: Can we convert local PL to Global PL?</b></br>
**A:** ✅ Yes, we can. Salesforce allows converting a **Local Picklist** to a **Global Value Set**.

<b> Major difference while working on local and global PL? (Nokia)</b></br>
**A:** 
* In **Local Picklists**, you can **enable custom settings** such as:

  * **Restrict picklist to the values defined** (optional).
  * **Add unique values per object**.
* In **Global Picklists**, the value options are **centrally managed** and **restricted** to the defined global set.
* Any change to a **Global Value Set** reflects across **all dependent picklist fields** using it.

#### Important Notes:-
#### Limits and Useful Points for Global Picklists

| Limit / Feature                                               | Description                                           |
| ------------------------------------------------------------- | ----------------------------------------------------- |
| **Global Picklists per Org**                                  | Up to **500** Global Picklists                        |
| **Values per Global Picklist**                                | Up to **1,000 active/inactive values**                |
| **Number of Local Picklists referencing one Global Picklist** | **Unlimited**                                         |


## Field Dependency
In Salesforce, field dependency refers to the relationship between two fields on a Salesforce object where the values available in one field depend on the value selected in another field. This feature allows you to create dynamic behavior in your Salesforce application based on the selections made by users.

In field dependency, there will be only 2 types of fields:</br>
1. Controlling field (primary)</br>
2. Dependent field (secondary)</br>

<b>Q. Which all are valid fields for field dependency?</b></br>
A. Picklist, Picklist (multiselect), Checkbox

<b>Q. Which fields can be used as Controlling field? (Infosys)</b></br>
A. Picklist and Checkbox

<b>Q. Which fields can be used as a Dependent field? (Infosys)</b></br>
A. Picklist and Multiselect Picklist

Notes : 
- If you'll delete controlling field or dependent field and then undelete that field then field dependency will not retain.
- Hide or show Field is not possible.
- Hide or show values is possible.
- A picklist which are controlling can contain max <b>300</b> values, but a picklist which are dependent can contain max <b>1000</b> values.
- LOV = List of values (all values which will show in dropdown or you can say in picklist)
- if customer provide you a excel file than you can easly add all LOV by copy paste only.
- A picklist which is standalone that means not connected with any other fields then max value it can contain is <b>1000</b> only.
- In Salesforce, the maximum character limit for a single picklist value is 255 characters.
- In Salesforce multilevel dependencies are possible (Ex: Country -> State -> City )

<b>Q. What are the limitation of field dependency features ?(Disney)</b></br>
A. 1. all process need to done manually and when we have large amount of data like 200-300 records then this is not a easy solution. </br>
2. It is limited to only 3 types of fields (picklist, multiselect picklist, checkbox)</br>
3. after undelete dependency gone.</br>
4. Only control value of the field not able to control field itself.</br>

<b>Q. Country is controlling State. State is controlling City.</br>
Country = limit?</br>
State = limit?</br>
City = limit?</b></br>
A. Country = 300</br>
State = 300 </br>
City = 1000 </br>


<b>Q. If ur junior is facing limit issue while creating picklist of large data in ur project, then what can be the possible issues?</br>
(the field is NOT dependent of anything. no connection.)</b></br>
A. 1.LOVs going above 1000 count</br>

2. Characters exceeded more than 15k (IMP IQ)</br>
(Many people in market dont know this!!!)</br>

Means, assume, we have country PL with below values.</br>
India</br>
USA</br>
Canada</br>

(India(5) +USA(3) +Canada(6) ..etc ==> total char limit must be below 15k)</br>

current situation = 14/15000</br>

<b>Q. Have u seen this error in ur project? </br>
"the field you chose is directly or indirectly dependent on itself." </br>
When?</b></br>
A. when user will select controlling field and dependent field same.

<b></b></br>

## Formula Fields
- There is no such scope for user to enter the data in formula field, Formula field always copy the data from other field.
- In formula field target fields / Output filed can not be picklist and textarea.
- In formula field soruce field from where you are taking data can be picklist or textarea.
- Picklist = ISPICKVAL()
- Picklist Multi Select = INCLUDES()
- we can convert entire content into text with the help of TEXT() function.
- Today() -------> only current date
- Now() ---------> current date and time
- Formula fields can contain up to 3900 characters, including spaces, return characters (ENTER), and comments.
- 

- <b>Q. What is formula field?</b></br>
A.
  - This is a special type of field or advanced field
  - User can not make entry in this field.
  - data will be auto populated.
  - Data will be come from another field of from our business logic or some calculations but not directly from user.
  - This is also called as readonly field.
  - we can use cross object formula field. (COFF), when we copy data where the field present in other table, this is also possible

- <b>Which type of field can NOT become a Formula Field ?</br>
(select 2 wrong options)</br>
Text</br>
Number</br>
Percentage</br>
Picklist</br>
Text Area</b></br>
A. Textarea and Picklist


- <b>Q. What is limit of spanning relationships per object ?</b></br>
  A. 15 (spanning relationship means a bridge between two objects)


## Relationship in Salesforce

### Master Detail Relationship
A master-detail relationship in Salesforce is a type of relationship that tightly links two objects together, where one object (the master) controls certain behaviors of the other object (the detail). Here are the key points of a master-detail relationship in Salesforce:</br></br>
#### Key Characteristics of Master-Detail Relationships
**1. Parent-Child Relationship:** The master object is the parent, and the detail object is the child. The child object is always tightly linked to the parent. </br>
**2. Cascade Delete:** If a record in the master object is deleted, all related detail records are also deleted.</br>
**3. Ownership and Sharing:** Detail records inherit the owner and sharing settings of the master record. You cannot have different owners for the master and detail records.</br>
**4. Roll-Up Summary Fields:** You can create roll-up summary fields on the master object to perform calculations (sum, count, min, max) on the related detail records.</br>
**5. Field Limits:** Each object can have up to **2 master-detail** relationships</br>
**6. Standard Objects:** You cannot create a master-detail relationship where a standard object is the detail object. Standard objects can only be masters in master-detail relationships.</br>
**7. Reparenting:** By default, detail records cannot be reparented (i.e., assigned to a different master record). This behavior can be modified to allow reparenting by setting the "Allow reparenting" option during the relationship creation.</br>



- Relationship is to connect objects with each others in Salesforce
- In RTP (Real time project) very rarely you will create any isolated object in your career, most of the time you have to create relationship between them.
- Apart from 5 relationship in salesforce there is one more relationship in salesforce that is <b>External Lookup Relationship</b> which we will use to connect salesforce object with any external object or table (like Dotnet Software table)
- Below 2 lines will help you to make things clear
    - Student (Secondary Object) ---> Many Records
    - Mentor Teacher (Primary Object) ---> One Record
- Salesforce by default supports one to many connection, we need to do some extra efforts for one to one and many to many connection.
- In Lookup Relationship if we'll delete primary record then there is no effect on secondary record but in Master Detail Relationship if we'll delete primary record then secondary record will automatically deleted.
- If you'll delete any record from master detail relationship then as we know secondary record will delete, then the interesting thing is when we'll check recycle bin then we'll find only primary record which we have deleted secondary records are not visible there but in backend it is stored, because when you'll restore that deleted record from recycle bin then primary record will restore as well as all associated record which was deleted due to tightly coupled relationship will also restored.
- In MDR child record will be controlled by parent record. Owner field will not available in child record in MDR because parent record owner will be the owner of child record.
- In one object we can create either max 40 LR or max 2 MDR.
- In LR there is no concept of Roll-up Summary but in MDR there is a concept of Roll-up Summary.
- Reparenting feature is available in MDR with some extra effort by clicking a checkbox of Allow Reparenting. but in LR it is not required because in LR we can change it any time.
- Roll-Up Summary only activated for select when there is MDR and object should be Primary Object of MDR. else it will be show in readonly mode.
- In One object we can contain 40 Roll-up summary.
- We can not have Leads or Users at Master side in a Master-Detail relationship.
- If you want to check what type of relationship between two or more objects then you have to check that with the help of Schema Builder option which is available in setup.
- We can create or modify new object from Schema Builder, even we can add or delete fields of any object with the help of Schema Builder.
- ![Screenshot 2024-03-05 at 12 28 54 PM](https://github.com/therishabh/salesforce-notes/assets/7955435/d3b23d5e-4c4a-4c84-b939-91d94809d1fe)



<b>Q. What is Relationship in Salesforce ?</b></br>
A. Connecting two different objects with each others in salesforce. 

<b>Q. What are the types of Relationships in SF?</br>
or</br>
How we can connect objects in Salesforce? (IQ:Dell, Nokia, Puma)
</b></br>
A. Lookup Relationship</br>
B. Master-detail Relationship </br>
C. Many to many Relationship</br>
D. Hierarchical Relationship</br>
E. Self Relationship</br>

<b>Q. What are Lookup Relationship features ?</b></br>
A. - it use to connect objects in simple way</br>
- it works on standard object as well as custom objects</br>
- it works to loosly connect two objects.</br>

<b>Q. What are the problems with LR (Lookup Relationship)</b></br>
A. - if we want strong connection or mendatory connection then lookup relationship is not good.
- There is loose bond between objects.

<b>Q. What are the features of MDR</b></br>
A. - connect two objects with strong connection.
- If primary record deleted then secondary record will be automatically deleted. (this is called <b>Cascading Delete</b>)

<b>Q. What is Roll-up Summary ?</b></br>
A. - Roll up summary is a special field to show summary of child records.
- we can show summary like total count (total child records), max, min and sum.
- Only works with MDR and Parent object.
- in One object we can contain 40 roll up summary.

<b>Q. What is data skew / data skew error in Salesforce?</b></br>
A. This is a performance issue which comes into picture due to "limitation of Salesforce software", when one parent record will have more than 10k child records.

<b>Q. What types of fields we can have in the field to aggregate in Roll-up Summary ?</b></br>
A. Numerical Value (to be precise : number, currency, date, date and time, percentage)


<br>Rule in Salesforce:</br>
STANDARD OBJECTS CAN'T BE ON THE DETAIL SIDE WHEN IN MASTER SIDE ANY CUSTOM OBJECT IS PRESENT, IN MASTER-DETAIL RELATIONSHIP.</br>
(Read above line and tell me which scenario is NOT POSSIBLE in Salesforce projects!!)</br>
Scenario 1:</br>
Master = a custom object</br>
Detail = a standard object</br>

Scenario 2 :</br>
Master = a custom object</br>
Detail = a custom object</br>

Scenario 3 :</br>
Master = a standard object</br>
Detail = a standard object</br>

Scenario 4 :</br>
Master = a standard object</br>
Detail = a custom</b></br>
A. Scenario 1


<b>Q. What can be done using Schema Builder ?</b></br>
A. 

<b>Q. How to identify MDR or LR in Schema Builder ?</b></br>
A. MDR and LR we can decide by color of thread which are present between two objects, and three lines means child and one line means parent.

<b>Q. What is the relationship between Account and Contact object ? (Famous question based on exception in SF)</b></br>
A. Acc and Contact will have Lookup relationship by default.</br>
BUT,</br>
if u connect any record of Account to Contact, then they start behaving like MDR, because if Primary record is deleted then Secondary record will also get deleted. (this is managed by SF internally, so we dont need to do anything for this feature)

### Custom Labels Vs Custom Settings Vs Custom Metadata
#### What is Custom Label in Salesforce?
Custom labels are custom text values that can be accessed from Apex classes, Visualforce pages, or Lightning components. They are typically used for any text that needs to be translated into different languages, or custom text that might need to change frequently.

For example, you could use a custom label to store the error message text that’s displayed to users. If you need to change that message, you can just change the label, rather than editing and re-deploying your code.

#### What is Custom Setting in Salesforce?
Custom settings are similar to custom labels, but they’re used to store data that your org might need to reference frequently. They can store any kind of data, like numbers, strings, or dates, and can be used to create org-wide settings.

Use cases might include things like controlling behavior of your code (for instance, enabling or disabling features without changing the code), storing information that is used across multiple classes or triggers (like thresholds or constants), and reducing SOQL queries as data is cached and available across the org.

1) It is a way through which anyone can get easier and faster access to data.
2) The main advantage of using Custom Settings is that the data is cached, which enables efficient access without the cost of repeated queries to the database.One doesn't have to use SOQL queries which count against the governor limits.
3) Custom settings data can be used by formula fields, Visualforce, Apex, and the Web Services API.

**List Custom Setting**
1) It provides a reusable set of static data which can be accessed across your organization.
2) The data in List Custom Settings is directly visible to any user in the org.
Eg: Let's suppose we want to add custom settings of phone codes of countries. For example, if someone chooses India, automatically a +91 number initiates in the form, thus, it is not necessary to fetch from the database by using SOQL query in the backend. So, let's fill the label and object name accordingly. We will choose the setting type as List.

#### What is Custom Metadata in Salesforce?
Custom Metadata Types stores the records in a memory cache which allows faster retrieval of data when you execute a query. 

Custom Metadata Types in Salesforce are similar to custom objects. It has a suffix of “__mdt” instead of “__c” in the API namespace. Let’s say if you create a Custom Metadata type with name “Apex Hours”, the API name of the metadata type would appear as – “Apex_Hours__mdt”.

- This doesn’t count against Governor limits.
- It are deployable from one environment(Org) to another environment. You can package your metadata along with data or deploy it easily from one Org to another. 

For more detail : https://www.apexhours.com/custom-metadata-types/

## Lightning Flow
- Flow is very powerful tool which is available in salesforce.
- Flow Provides declarative process automation.
- In Salesforce there are two types of development
    - Declarative development
    - Custom development
- Declarative development is also known as low code development.
- Lightning Flow provides this point and click automation tool i.e. **Flow Builder**
- Lightning Flow is a product, process build and flow builders are name of the tools.
- If you talk about the product then it's Lightning flow and if you talk about the tool with which you'll be implement the flow so that is flow builder.
- **Work flow and process builder are getting retired, they are deprecated now.**

## Security
- Security topic = (this is not a single topic, this is group of topics!!!)
    - External Security
    - IP setting
    - Password reset
    - Audit trail
    - User Management
    - Internal Security
    - OWD
    - Profile
    - Permission set
    - Roles
    - Sharing Rules
    - Manual Sharing
    - Field Level Security
    - Queue
    - Public Group

#### User License
- In Salesforce we have multiple licenses but 2 license is very famous i.e. Salesforce License and Salesforce Platform License.
- Salesforce software for learning purpose so obviously giving limited Licenses, salesforce provide only 2 license for Salesforce and 3 license for Salesforce Platform.
- User License is main License and there are few checkbox in user setup those are secondary License or we can say featured License.
  
  ![image](https://github.com/therishabh/salesforce-notes/assets/7955435/1ef77a99-9f6c-4ebf-a832-6a1b80b8af00)
  
- How many License we have ? we can check that by typing Company information in quick search in setup, then scroll down and there is a section of User Licenses in that section we can check all available Licenses and used Licenses.
  
  ![Screenshot 2024-03-12 at 5 43 39 AM](https://github.com/therishabh/salesforce-notes/assets/7955435/7dc4af45-0cf1-4198-8371-f7492a98580b)

-  What are the difference between Salesforce and Salesforce Platform License ?
    - Answer
      | Salesforce License    | Salesforce Platform License |
      | -------- | ------- |
      | Any Standard Object  | Can work on few Standard Object    |
      | Can work on any custom Object | Can work on any custom Object     |

- Which is the most costly License salesforce or salesforce platform ? (Answer : Salesforce License)
- What situation you will recommend your client to use salesforce platform License ? (Answer : Budget issue, and entire requiment will be fullfill by custom object then salesforce platform License is sufficient)
- What are the different ways to reset the password in salesforce ?
    - Answer :
      - Company Level
      - Department Level
      - User Level
      
- In the real time project how many licenses do we need to purchance to inform client ? (Answer : We should ask with client that how many people are there, as per that we need to do the needful)
- can we delete the user in salesforce ? (Answer : No)
- Why we can not delete user from salesforce ?
    - Answer :
      - Salesforce user have connection with various possible settings in salesforce software which can collapse if user will deleted
      - User connection to various business responsibilities which can damage salesforce org integrity
      - if user changes some data and if we delete that user then how we can track who delete what data.
- For example, salesforce licence cost $50 to $300 per user per month and there are 10 people resign today so how we can save money as you said we can not delete user ? (Answer : just deactivate user by edit user option and remove checkbox from active then save)
- There is a option available in user section that is <b>Freeze</b>, which is similar to deactive user not exact same, by Freeze we can block a user to login, from making entry into the salesforce org.

#### OWD (Organization Wide Defaults)

- OWD is a initial level of setting we do for every object while doing Security. In other words OWD is a setting by which we can decide how records of a specific object can be availble for all the users in the company except the owner.
- What are "key" types of OWD settings in Salesforce ?
    - Answer
        - Public Read and Write
        - Public Read Only
        - Private
- In OWD we will perform action which will impact complete organization.
- Admin can login any user from users section in setup, firstly admin need to be activate Login Access Policy then login link will be visible in users section.
  
  ![Screenshot 2024-03-12 at 7 24 39 AM](https://github.com/therishabh/salesforce-notes/assets/7955435/9ff1e8c7-49d0-4891-958e-60e91903a5eb)

- When any user will login from users section as maintioned above and after logout that user admin should be still login, but by default when you'll logout from user then admin will also logout, to maintain this session we have to change in session setting section under setup. (You have to uncheck "Force relogin after Login-As User")

  <img width="876" alt="Screenshot 2024-03-12 at 12 34 34 PM" src="https://github.com/therishabh/salesforce-notes/assets/7955435/dad4956d-ee81-442d-a765-9176cc5af169">
  
- Most of the companies salesforce Unlimited addition using. (all the features of salesforce)
- In salesforce project creator of any record is not such useful, compared to Owner of that record. Owner is responsible of his record, creator will not responsible.
- We can change OWD setting from Sharing Settings section to change object Default Internal Access. By default Defaul Internal access is Public Read and Write.

  ![Screenshot 2024-03-12 at 12 45 00 PM](https://github.com/therishabh/salesforce-notes/assets/7955435/3f62490b-9885-49fc-b388-a4df93c75a84)

-  In OWD delete facility is not possible only view and edit facility is possible.
-  Issue :
    - whatever setting we do, it applies for everyon in the company we can not set things for few people.
    - We can not give delete facility by OWD.

#### Profile
- What is Profile, and when we have things like OWD, why we need Profiles ?
  - Answer : In OWD, we can make selective sharing of data accessibility hence we need to use Profile. Profile is a collection of some rules which help us to improve some Implement some restrictions some rules and regulations in a group of people and it's not going to make a flat impact on entire company in short we have flexibility which is absence which is absent in OWD.

#### Permission Sets
- In profile we are doing clone of profile with another profile but in permission sets we don't need to clone it, we can create fresh permission sets
- What is Permission Sets ?
    - Permission Sets are the extensions to the Profiles !
    - Permission sets is only for giving not for taking out the access which user already has.
- What are the benefits of Permission Sets ?
    - We can have only one profile for one user by default but here in permission set we don't have that problem, one person can have 3 permission sets, 300 permission sets and so on.
    - In Profile we can add only that user which having matching license but in permission sets we can add, a person which have Salesforce License also, a person which have Salesforce Platform license also.
    - In Profile is something we use to give a same level of setting for all the users in the department but in permission sets is for different different settings for different different users.
- In one saleforce Org how many permission set we can create ? (Answer : Approx 1000)
- Salesforce decided in future more focus on Permission sets and less focus on Profile.
- if you want to disable setup option on any user then there is an option in profile "View Setup and configuration" you should deselect that option.
- Fill in the blanks: (20 sec)
    - OWD = impacts "entire xxx" FOR THAT OBJECT (xxx = organization)
    - Profile = impacts "entire yyy" FOR THAT OBJECT (yyy = department)
    - P'set = impacts only "specific zzz" from a dept FOR THAT OBJECT (zzz = user)
- Object should be private in OWD (99.99% objects)

#### Role
- If you'll close the door (remove permissions) for any user from OWD, then profile and Permission sets and by Role we can give permission to that user to access the data.
- What is significance of role?
    - In a project if OWD of object is private as well as there is no admin level access like profile, permission sets still the senior level person can access the record owned by Junior, how by role facility.
- What is the access level the senior can get on records shared by Roles? (Answer : RED Read-Edit-Delete)
- Suppose there is a user (A), and he has one junior person (B) under his role although person A is not able to see records of his junior person. for this, main reason is under OWD there is an option Grant Access Using Hierarchies should be enabled.
  
  ![Screenshot 2024-03-16 at 9 06 11 AM](https://github.com/therishabh/salesforce-notes/assets/7955435/24e6a3d2-c106-4af2-9781-a980c27de4a2)

- Any Salesforce org created in 2022 or later, the count of role became 10000, for older org, the maximum number of roles allowed is 500 only.

#### Sharing Rules
- While working on sharing rules currency field is not supported.
- ![Screenshot 2024-03-16 at 2 53 40 PM](https://github.com/therishabh/salesforce-notes/assets/7955435/39301a7e-0809-4807-b20a-8db5348f3325)

- What is sharing rules ?
    - To share the records, based on some conditions, we use SR. (dynamic sharing) [This is called as selective sharing]
- What are the different types of Sharing rules ?
    - Owner based and criteria based.
- Permission available in sharing rules (Read and Read/Write)
- In sharing rules, previous records also shared based on criteria which you have selected.
- problems with sharing rules ?
    - we have some selected fields in sharing rules (suppose we can not select criteria base on currency field)
    - Sharing rules does not give permission to delete the record only edit or view permission we can provide.
    - We can not share record with a single person.
--------------------------

### Levels of Data Access
- Organization
- Objects
- Fields
- Records

### Organization
- Maintain a list of authorized users
- Set password policies
- Limit login to certain hours and locations
  - Limit IP Addresses from which users can log in
  - Limit the times at which users can log in

### Object Level Security
- You can control object level permissions for both Standard and Custom Objects.
- You can set permissions for a particular object.
- You can give permissions to view, create, edit and delete any records of that object.
- You can control object permissions using profiles and permission sets.

### Field Level Security
- You can restrict access to certain fields in Salesforce, even if user has object level access.
- You can make a field visible to a particular user and can hide that from another user.
- You can give Read or Edit permission to a field, if you don't give both then that field will not be visible.
- Field Level Security can be controlled using Profiles and Permission
Sets.

### Profile
- A profile is a collection of settings and permissions.
- Profile settings determine which data the user can see, and permissions determine what the user can do with that data.
- A profile can be assigned to many users, but a user can have only one profile at a time.
- To create new profile you need to clone existing profile.

### Permission Set
- A permission set is a collection of settings and permissions that give user access to various tools and functions.
- Permission sets extend users functional access without changing their profile.
- Through Permission sets permission can be granted and any time it can be taken away as well.
- Users can have only one profile, but they can have multiple permission sets assigned.

### Permission Set Group
- Permission Set group bundles different permission sets together based on a persona.
- A permission set group includes all the permissions available in the permission sets.
- One permission set can be included in more than one permission set groups.
- A user can be assigned one or more Permission Set Groups.
- Also we can assign Permission Set and Permission Set Groups together to users.

### What is MUTE in Permission Set Group?
- One can mute some permissions in Permission Set Groups so that they won't be given to the user.
- If you mute particular permission in Permission Set Group then it won't impact individual Permission Set, they remain intact.
- You can anytime unmute the permissions in permission set group.

### Record Level Security
- You can restrict access to records for users, even if user has object level permissions.
- For example, a user can view his own records but not others.
- You can manage Record Level Access in following ways:
  • Organization-wide defaults</br>
  • Role hierarchies</br>
  • Sharing rules</br>
  • Manual sharing</br>
![image](https://github.com/therishabh/salesforce-admin/assets/7955435/0b245f0c-f892-473d-a9e6-2d836737660d)

### Organization-wide defaults
- It specified the default level of access of records.
- Org-wide sharing setting lock down the data to the most restrictive level.
- Here you have three access level:
  • Private</br>
  • Public Read-Only</br>
  • Public Read/Write</br>
- You can use other Record Level security and sharing tools to open up the sharing of records.

### Role Hierarchies
- It gives access for users higher in the hierarchy.
- That user can access all records owned by the users below them in the hierarchy.
- Each role in the hierarchy should represent a level of data access that a user or group of user needs.

### Sharing Rules
- These are exceptions to Org-Wide defaults.
- Through sharing rules you can share records to a group of users.
- So that, they can get access to the records they don't own or can't manually see.

### Manual Sharing
- It allows owners of particular records to share them with another userS.
- Manual sharing is not automated like Org-wide defaults, Role hierarchy or sharing rules.
- It can be useful in some situation where you manually want to share a record with another user.

<img width="1440" alt="Screenshot 2024-08-05 at 8 50 26 AM" src="https://github.com/user-attachments/assets/b5462c2e-f88a-46bb-8c3c-f2f575a41c9b">

<img width="1440" alt="Screenshot 2024-08-05 at 8 50 43 AM" src="https://github.com/user-attachments/assets/b00dcd7a-77d0-4e7a-908b-98d9b10549e8">

<img width="1440" alt="Screenshot 2024-08-05 at 8 54 10 AM" src="https://github.com/user-attachments/assets/b194546f-cf62-4cc6-b20e-2f4ba1a8c764">

<img width="1440" alt="Screenshot 2024-08-05 at 8 53 50 AM" src="https://github.com/user-attachments/assets/5496b4f4-972c-4281-9b4b-a1058814bf24">

<img width="1440" alt="Screenshot 2024-08-05 at 8 55 49 AM" src="https://github.com/user-attachments/assets/42c2960d-3cdb-4b29-a695-dacbabe7a7f8">

<img width="1440" alt="Screenshot 2024-08-05 at 9 01 02 AM" src="https://github.com/user-attachments/assets/9186f95c-6196-4b61-a090-5157883cd6aa">

<img width="1440" alt="Screenshot 2024-08-05 at 9 01 30 AM" src="https://github.com/user-attachments/assets/b6c1c6eb-ae40-44df-82f7-3e8ce0e5d8a7">

<img width="1440" alt="Screenshot 2024-08-05 at 9 04 46 AM" src="https://github.com/user-attachments/assets/5dee6782-c520-4750-bc0f-591d17f198b2">

<img width="1440" alt="Screenshot 2024-08-05 at 9 05 00 AM" src="https://github.com/user-attachments/assets/dee9b453-15c2-4ea2-adc8-d2fe98920f19">

<img width="1440" alt="Screenshot 2024-08-05 at 9 06 44 AM" src="https://github.com/user-attachments/assets/aa2a6893-a629-49a5-9f56-94095f276ed5">

<img width="1440" alt="Screenshot 2024-08-05 at 9 19 09 AM" src="https://github.com/user-attachments/assets/8a359f13-7945-4d84-b9cb-abeb875abfe6">

<img width="1440" alt="Screenshot 2024-08-05 at 9 20 55 AM" src="https://github.com/user-attachments/assets/ff102167-3f28-44a6-86ef-df0a55017067">

<img width="1440" alt="Screenshot 2024-08-05 at 9 24 37 AM" src="https://github.com/user-attachments/assets/48f99ebe-2b38-44aa-9aaf-905b3eb8cb1e">

<img width="1440" alt="Screenshot 2024-08-05 at 9 27 11 AM" src="https://github.com/user-attachments/assets/d4124063-7b0c-4573-a09d-c7ca5c9d5a8a">

<img width="1440" alt="Screenshot 2024-08-05 at 9 27 26 AM" src="https://github.com/user-attachments/assets/0cf2d8cc-cb3e-4796-acc7-1bcdf884a4b7">

<img width="1440" alt="Screenshot 2024-08-05 at 9 34 00 AM" src="https://github.com/user-attachments/assets/3eae73c8-16d5-4a4f-9ece-ac3e585f6bc4">

<img width="1440" alt="Screenshot 2024-08-05 at 9 34 09 AM" src="https://github.com/user-attachments/assets/72186c62-851d-44c1-90e6-edbbe4f333ac">

<img width="1440" alt="Screenshot 2024-08-05 at 9 38 17 AM" src="https://github.com/user-attachments/assets/48d91ee5-004b-4e59-a70d-f48bb122d76c">

<img width="1440" alt="Screenshot 2024-08-05 at 9 41 46 AM" src="https://github.com/user-attachments/assets/72bc086d-95e6-4d26-8a42-1ae144773677">

<img width="1440" alt="Screenshot 2024-08-05 at 9 42 04 AM" src="https://github.com/user-attachments/assets/6af3b224-8b9d-41b1-a6b3-e01f86bd9038">

<img width="1440" alt="Screenshot 2024-08-05 at 9 42 15 AM" src="https://github.com/user-attachments/assets/bba0bc71-f096-4141-912b-56e676bc6222">

<img width="1440" alt="Screenshot 2024-08-05 at 9 42 33 AM" src="https://github.com/user-attachments/assets/bc96ee55-2b6f-46c9-bf07-59be981bb2a4">

<img width="1440" alt="Screenshot 2024-08-05 at 11 01 39 AM" src="https://github.com/user-attachments/assets/1bf24a12-c02d-4312-b751-4ed9a09e7d55">














