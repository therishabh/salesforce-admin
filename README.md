# Notes

### Salesforce Basic
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

- when field will delete then it'll not show in detail page as well as it will not show in history section.
- after recover any field from delete all data will be maintain in history section. (dell)

#### Important Rules
- If we create a field with text and set its behavior to 'unique,' it will work fine as expected. However, if someone accidentally deletes that field and then recovers it, it will lose its uniqueness property.
- If we have a field with the required property, it will work fine as expected when creating a new record. However, if someone accidentally deletes that field and then recovers it, it will lose its visibility and required property. This means that the field will not be visible after being undeleted, and we will have to set its visibility from the Set-Field-Level-Security section and mark it as required from the Edit section.
- If we have a custom field, it will work fine. However, if someone accidentally deletes that field and later changes the page layout, when the user recovers that field from deletion, it may not be visible in the form as expected. To fix this issue, we need to check the page layout and drag and drop the field to a suitable place.


<b></b></br>
<b></b></br>
<b></b></br>
<b></b></br>
<b></b></br>




