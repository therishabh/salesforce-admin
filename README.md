# Notes

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

## Field Tracking
<b>Q. What are the benefits of field tracking in ur job?</b><br />
A. 

<b>Q. Can we track standard fields ? (TCS) </b><br />
A. Yes, Only 2 fields we can track [Owner and Name (Auto Number)]

<b>Q. Which standard fields we can not trackt and why ?</b> <br/>
A. CreatedBy and LastModifiedBy <br/>
  Reason: creation record happens only one time thats why Salesforce not provide that facility to track createdBy lastModifiedBy will change complete data we can not track by lastModifiedBy like who change which data and second reason is data is changing very frequently so lastModifiedBy will change many time so Salesforce think there will be no sense to track lastModifiedBy

<b>Q. What are the issues you face when you depend on data of "Last modified by" to track the data change? Is that totally reliable?(IBM)</b></br>
A. Last modified by only show who change or modify the fields but with that field we can not track which field is changed, so it's not reliable.

<b>Q. If your junior is asking you that he is not able to see field tracking details in related section, what u will do? </br>
OR</br>
By what all reasons we can not track the field changes?</b></br>
A. 

<b>Q. Field tracking helps us to see only "xxx changes". Not "yyy changes".</b></br>
A. xxx = data, yyy = settings 

<b>Q. History tracking feature tracks new and old value for most of the fields but for some fields, it will not do such check. It will only show "Changed xxxxx."
(xxxx = field name)</b></br>
A. Formula Fields, Encrypted Fields,  Rich textfield, long textfield, multiselect picklist, more than 255 character field

<b>Q. For which custom field (below 255 length) we can not have field tracking?(Infosys)</b></br>
A. Formula Field, Auto Number, Role of summary.

<b>Q. Data in history table, how long we can retain that data (Disney)</b></br>
A. 18 months without coding, with coding we can retain 24 months.</br>
<b>Field history tracking data doesn't count against your Salesforce org's data storage limits.</b></br>

<b>Q. How many fields we can track per object? (Chase Bank)</b><br/>
A. 20 fields

## Field Deletion consideration 
<b>Q. Recycle Bin of records Vs Recycle Bin of fields : (Amazon)</br>
1.Difference </br>
2.Common thing
</b> </br>
A. delete of any record we can see in recycle bin while delete of any field we can see in deleted field under Fields & Relationships section. as you delete any record or field then they both go to into recycle bin area and wait for 15 days after that data or field will be permanently deleted.</br>
<b>After 15 days, data is permanently deleted from the Recycle Bin</b>

- if you want to free some space by deleting the field then you have to delete those field by permanently otherwise space will not free. (best practice)
- you can check limitation and usase of custom field by go to Object Limits under object manager.

<b>Q. After undelete of fields, are values recovered? (Puma)</b></br>
A. Yes values recovered.

- When a field is deleted, it will not show on the detail page, nor will it appear in the history section.
- After recovering any field from deletion, all data will be maintained in the history section. (dell)
- Object deleted, Field deleted - we can recover.
- App Deleted - we can not recover.

#### Important Rules
- If we create a field with text and set its behavior to 'unique,' it will work fine as expected. However, if someone accidentally deletes that field and then recovers it, it will lose its uniqueness property.
- If we have a field with the required property, it will work fine as expected when creating a new record. However, if someone accidentally deletes that field and then recovers it, it will lose its visibility and required property. This means that the field will not be visible after being undeleted, and we will have to set its visibility from the Set-Field-Level-Security section and mark it as required from the Edit section.
- If we have a custom field, it will work fine. However, if someone accidentally deletes that field and later changes the page layout, when the user recovers that field from deletion, it may not be visible in the form as expected. To fix this issue, we need to check the page layout and drag and drop the field to a suitable place.

## Global Picklist
- Global picklist or Global value set or Picklist value set

How to decide when we need to create a local or a global PL?</br>
- Becoming proactive in ur project</br>
- Check requirement doc neatly</br>
- Asking BA

<b>Q. Can we convert local PL to Global PL?</b></br>
A. Yes.

<b>Q.Major difference while working on local and global PL? (Nokia)</b></br>
A. in local picklist we can enable 

#### Important Notes:-
- Limit | Useful Points for global picklist:</br>
   - 1 Org = 500 GPL
   - 1 GPL = Upto 1k active/inactive values
   - Number of local PLs for 1 GPL = No limit


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
- 
 










