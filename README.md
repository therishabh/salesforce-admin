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





