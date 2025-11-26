---
nav_title: Uploading CSV Files
article_title: Data Ingestion - Uploading CSV Files - User Guide
page_order: 11
layout: doc_guide
page_collection: 'user_guide'
article_title: Dataroid User Guide
---

# User Property Ingestion - CSV Upload

Understand how to ingest properties to user profiles using the **User Property Ingestion - CSV Upload** feature.

You can bulk-create or update user profile properties in Dataroid by uploading CSV files.

{% alert tip %}
Anyone with the **required permissions** can use this feature.

* Admin users can create Integrations.
* An API Key is required to upload CSV files.
{% endalert %}


## Upload User Properties using a CSV File
To upload user properties to the Dataroid using a CSV file:

1. Generate file structure.  
2. Map user properties to create an integration.  
3. Generate Upload URL (Signed URL).  
4. Upload the CSV via a Signed URL.

### Step 1. Generate File Structure

Before mapping user properties, you must prepare the CSV structure. For more information on the CSV file format, refer to the [CSV File Format](#csv-file-format) section.

Below is an example of a CSV file:

{% tabs local  %}
{% tab csv file content %}

```
Customer Id,Employment Status,Education status,Credit Point,DOB,Campaign ID,CMP 764
320736874602,true,Graduate,1699,810680400,CMP_80,eligible
631943793507,FALSE,Graduate,1699,463611600,CMP_80,not eligible
405170815060,0,Graduate,1900,-167540400,CMP_80,not eligible
762854554643,TRUE,Graduate,1900,-419997600,CMP_80,not eligible
325476867866,false,Graduate,1800,-415159200,CMP_80,not eligible
132009822655,1,Graduate,1500,1604523600,CMP_80,eligible
```

{% endtab %}
{% tab preview %}

Customer Id | Employment Status | Education status | Credit Point | DOB | Campaign ID | CMP 764 |
---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
320736874602 | true | Graduate | 1699 | 810680400 | CMP\_80 | eligible |
631943793507 | FALSE | Graduate | 1699 | 463611600 | CMP\_80 | not eligible |
405170815060 | 0 | Graduate | 1900 | \-167540400 | CMP\_80 | not eligible |
762854554643 | TRUE | Graduate | 1900 | \-419997600 | CMP\_80 | not eligible |
325476867866 | false | Graduate | 1800 | \-415159200 | CMP\_80 | not eligible |
132009822655 | 1 | Graduate | 1500 | 1604523600 | CMP\_80 | eligible |

{% endtab %}
{% endtabs %}

{% alert important %}
The ``Customer Id`` field is a mandatory case-sensitive column and must be exactly named as shown.
{% endalert %}


For the CSV file above, the property mapping would be:

| Column Name | User Property Name | Datatype |
| :---- | :---- | :---- |
| Employment Status | empl\_status | Boolean |
| Education status | edu\_status | Alphanumeric |
| Credit Point | credit\_point | Numeric |
| DOB | dob | Date |
| Campaign ID | camp\_1 | Alphanumeric |
| CMP 764 | cmp\_764 | Alphanumeric |

### Step 2. Map User Properties to Create an Integration

To map the CSV columns with the user properties:

1. Login to your Dataroid account and click Side Menu > **Data Ingestion**
{% lightbox /_site/assets/img/user_guides/property_ingestion/property_ingestion_step1.png --data="group1" --title="Map User Properties to Create an Integration - Step 1" %}

2. Click **+ New Integration** button. The **Mapping Property** page appears.  
{% lightbox /_site/assets/img/user_guides/property_ingestion/property_ingestion_step2.png --data="group1" --title="Map User Properties to Create an Integration - Step 2" %}
3. Map the CSV columns you prepared to either existing user properties or create new ones. Assign the correct data types for each.
   For the sample CSV structure, here is the example mapping:
{% lightbox /_site/assets/img/user_guides/property_ingestion/property_ingestion_step3.png --data="group1" --title="Map User Properties to Create an Integration - Step 3" %}
4. After saving the mapping, click **Submit** to activate the integration. Once you have submitted the mapping, you have an active ``Integration Id`` to [generate upload URL](#step-3-generate-upload-url-signed-url).
{% lightbox /_site/assets/img/user_guides/property_ingestion/property_ingestion_step4.png --data="group1" --title="Map User Properties to Create an Integration - Step 4" %}

{% alert tip %}
* Integration status can be either ``DRAFT`` or ``ACTIVE``
* If you realize a new column was added (e.g., “LoyaltyTier”) and you forgot to map it, you must edit or recreate the integration mapping before uploading the CSV file. If you try to upload the CSV without proper mapping, newly added column will not be ingested.
{% endalert %}


### Step 3. Generate Upload URL (Signed URL)
To upload a CSV file, you need a Signed URL.

Refer to the [Get Upload URL API](/repository/dataroid-docs/_site/api_reference/API_references/UserPropertyIngestion/Generate_Upload_Link.html) documentation for details.

{% alert tip %}
* To use this API, you must authenticate via an API Key as explained in the [API Authentication](/repository/dataroid-docs/_site/api_reference/API_references/home.html#authentication) documentation.  
* Multiple Signed URLs can be generated at the same time. They do not affect each other.  
  *e.g. you want to run multiple parallel uploads for different batches of users— one CSV file for premium users and another for standard users— you can generate two separate Signed URLs and upload each file independently*
{% endalert %}


### Step 4. Upload the CSV via Signed URL
After obtaining the Signed URL (upload url), you can upload the CSV file.

Refer to the [Upload CSV File API](/repository/dataroid-docs/_site/api_reference/API_references/UserPropertyIngestion/Upload_CSV_File.html) documentation for details.

Once the file is uploaded, Dataroid will notify the integration creator via email about the upload status. For more details, see [File Upload Status](#file-upload-status).

{% alert note %}
* The Signed URL is time-limited.  
* The last file sent to a single Signed URL overwrites previous uploads.  
* After 5 minutes, the given URL expires.  
* Authentication is managed through the signature on the Signed URL.
{% endalert %}


## Key Points to Remember

### CSV Upload Details

* If an existing user property is uploaded, its old value is updated with the new one.  
* If a new user profile property is uploaded, a new property is created on the user profile.  
* You can upload multiple CSV files simultaneously, even while others are processing.

After the upload is complete, the following information is displayed:

Field | Description
-- | --
Name | The CSV import name.
Uploaded date | The date when the CSV file was uploaded.
Status | See [File Upload Status](#file-upload-status) for details.
Errors | Count of rows not uploaded due to errors.
Processed | Count of rows successfully uploaded.
Not Found | Count of rows with a ``Customer Id`` not found in Dataroid.

### File Upload Status

After you send the file, Dataroid validates it according to the mapping rules. If valid, it begins processing. The possible statuses are:

| Status | Description |
| ---- | ---- |
| REJECTED | The uploaded file is not valid. It has been rejected and will not be processed.|
| ACCEPTED | The uploaded file is valid and accepted for processing. |
| PROCESSING | The user properties are currently being processed into the system. |
| FAILED | A system issue occurred while processing. You may try uploading the file again. |
| COMPLETED | The properties have been successfully processed into the system. Processing is complete. |
{: .reset-td-br-1 .reset-td-br-4}

#### Possible Rejection Scenarios:
 - File type is not CSV.
 - The ``Customer Id`` column does not exist.
 - Column mappings are not valid according to the given property mapping rules.
 - There is no column other than ``Customer Id``.

#### Error Reasons:
 - Corrupted file.
 - ``Customer Id`` does not exist in Dataroid.
 - Duplicate ``Customer Id``s exist in the same file. One is processed, others are ignored.
 - Property type is not valid (cannot be cast to the intended data type).

### CSV File Format

* Uploads are only allowed if the file is in CSV format.  
* You must adhere to CSV standards for successful processing.  
* There should be no duplicate ``Customer Id``s in the same file. If duplicates exist, one will be processed and the others ignored.

{% alert important %}
The ``Customer Id`` field is a mandatory case-sensitive column and must be exactly named as shown.
{% endalert %}

{% alert note %}
You can upload CSV files up to 1 GB in size.
{% endalert %}



### Data Types

Select a data type from the dropdown list for the property values. For instance, Credit Point has the value “1699” and is of the **Numeric** data type.

Data Type | Format | Description
--- | --- | ---
Date | Unix (epoch) | A timestamp or a count of seconds. For example, 1695799434. It measures time by the number of seconds that have elapsed since 00:00:00 UTC on 1 January 1970. All other formats will be treated as a String.
Numeric | Integer or Double | An integer value for data such as an Amount, Wallet Balance, Credit Point etc.
Numeric | Integer or Double | An integer or decimal value for data such as Amount, Wallet Balance, Credit Point, etc. Decimal values are accepted and must use a period ``.`` as the decimal separator (e.g., ``1234.56``).
Alphanumeric | String | A string value consisting of letters and numerals for data such as ``customer_type``, ``membership_level``, etc. For example, the membership level must be in the format ``BASIC``, ``PREMIUM``, or ``VIP``, and is treated as Alphanumeric.
Boolean | Boolean or Integer | A boolean value is, for example, True, which indicates if an email ID exists for users. Accepted formats: true, false (case insensitive), 0, 1.
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-4}


## FAQ

**Q: What happens if the same ``Customer Id`` appears multiple times in the file?**  
A: Only one record will be processed, chosen randomly. The other duplicates will be ignored.

**Q: What happens if multiple files are sent to the same Signed URL?**  
A: The last file sent to the Signed URL will overwrite the previous ones.

**Q: Is there a daily upload limit?**  
A: Yes, the daily upload limit is configurable based on your license. Please contact your Customer Success Manager for details.

**Q: Does a rejected file count toward the daily upload limit?**  
A: No, rejected files do not count toward the daily limit.

**Q: Are property values case-sensitive?**  
A: Yes, property values are case-sensitive. Please make sure to provide the correct formatting for the best experience.

**Q: What happens if the ``Customer Id`` column is empty, even if other columns are filled?**  
A: The file will be rejected.

**Q: What happens if a file is uploaded without the ``Customer Id`` column?**  
A: The file will be rejected.
