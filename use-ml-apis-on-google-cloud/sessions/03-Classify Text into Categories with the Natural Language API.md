# 🧠 Lab Session (Premium)

**Classify Text into Categories with the Natural Language API**

> Google Cloud Self‑Paced Lab (GSP063)
> Level: Intermediate | Duration: ~1 hour

---

## 🎯 Objectives

- Enable the Cloud Natural Language API
- Classify text documents into content categories
- Process long text inputs
- Store and analyze results in BigQuery

---

## ✅ Prerequisites

- Active Google Cloud Skills Boost lab
- Cloud Shell access

---

## 🔹 Task 0 – Start the Lab & Open Cloud Shell

```bash
gcloud auth list
gcloud config list project
```
![startlab](../screenshots/03_startlab.png)
---

## 🔹 Task 1 – Enable Cloud Natural Language API

APIs & Services → Library → Cloud Natural Language API → Enable
![Enabled_API](../screenshots/03_Cloud_NL_API.png)

---

## 🔹 Task 2 – Create an API Key

Since you're using curl to send a request to the Natural Language API, you need to generate an API key to pass in the request URL.

- To create an API key, in your Console, click Navigation menu > APIs & Services > Credentials.

- Then click Create Credentials.

- In the drop down menu, select API key.

Next, copy the key you just generated, then click Close.
![API_KY](../screenshots/03_APKY.png)

Now that you have an API key, you save it as an environment variable to avoid having to insert the value of your API key in each request.

In order to perform next steps please connect to the instance provisioned for you via ssh.

- Open the Navigation menu and select Compute Engine > VM Instances. You should see a provisioned linux-instance.
Click on the SSH button. You are brought to an interactive shell.

In the command line, enter in the following, replacing <YOUR_API_KEY> with the key you just copied:

```bash
export API_KEY=YOUR_API_KEY
```
![ExportAPI](../screenshots/03_ExportAPI.png)

---

## 🔹 Task 3 – Classify Text

-Create a file named `request.json` and add the code found below. You can create the file using one of your preferred command line editors (nano, vim, emacs).

```bash
{
  "document":{
    "type":"PLAIN_TEXT",
    "content":"A Smoky Lobster Salad With a Tapa Twist. This spin on the Spanish pulpo a la gallega skips the octopus, but keeps the sea salt, olive oil, pimentón and boiled potatoes."
  }
}
```
- Now you can send this text to the Natural Language API's classifyText method with the following curl command:

```bash
curl "https://language.googleapis.com/v1/documents:classifyText?key=${API_KEY}" \
  -s -X POST -H "Content-Type: application/json" --data-binary @request.json
```
- Run the following command to save the response in a result.json file:
```bash
curl "https://language.googleapis.com/v1/documents:classifyText?key=${API_KEY}" \
  -s -X POST -H "Content-Type: application/json" --data-binary @request.json > result.json
```
The API returned 2 categories for this text:

- /Food & Drink/Cooking & Recipes
- /Food & Drink/Food/Meat & Seafood

The text doesn't explicitly mention that this is a recipe or even that it includes seafood, but the API is able to categorize it. Classifying a single article is cool, but to really see the power of this feature, classify lots of text data.

![Classify](../screenshots/03_Report.png)

---

## 🔹 Task 4 – Store Result in BigQuery

- To see the type of text you'll be working with, run the following command to view one article (gsutil provides a command line interface for Cloud Storage):

```bash
bq mk news_dataset
bq mk --table news_dataset.results text:STRING,category:STRING,confidence:FLOAT
```

## 🔹 Task 5. Create a BigQuery table for categorized text data

Before sending the text to the Natural Language API, you need a place to store the text and category for each article.

- Navigate to Navigation menu > BigQuery in the Console.

- Click Done.

- To create a dataset, click on the View actions icon next to your Project ID and select Create dataset:
![alt text](../screenshots/03_BIGQUERY.png)

- The option 'Create dataset' highlighted within the View actions menu.

- Name the dataset news_classification_dataset, then click Create dataset.

- To create a table, click on the View actions icon next to the news_classification_dataset and select Create Table.

- Use the following settings for the new table:

  - Create table from: Empty table
  - Name your table: article_data

- Under Schema, click Add Field and add the following 3 fields:
![alt text](../screenshots/03_TABLE_BIGQUERY.png)


- Click Create Table.

The table is empty right now. In the next step you'll read the articles from Cloud Storage, send them to the Natural Language API for classification, and store the result in BigQuery.

![Table](../screenshots/03_Create_Table.png)
---

## 🔹 Task 6. Classify news data and store the result in BigQuery
In order to perform next steps please connect to the Cloud Shell. If prompted click continue.

Before writing a script to send the news data to the Natural Language API, you need to create a service account. This will be used to authenticate to the Natural Language API and BigQuery from a Python script.

1. Export your Project ID as an environment variable:
```export PROJECT=Project ID```
2. Run the following commands to create a service account:
```
gcloud iam service-accounts create my-account --display-name my-account
gcloud projects add-iam-policy-binding $PROJECT --member=serviceAccount:my-account@$PROJECT.iam.gserviceaccount.com --role=roles/bigquery.admin
gcloud projects add-iam-policy-binding $PROJECT --member=serviceAccount:my-account@$PROJECT.iam.gserviceaccount.com --role=roles/serviceusage.serviceUsageConsumer
gcloud iam service-accounts keys create key.json --iam-account=my-account@$PROJECT.iam.gserviceaccount.com
export GOOGLE_APPLICATION_CREDENTIALS=key.json
```
3. Write a Python script using the Python module for Google Cloud.
4. Create a file called `classify-text.py` and copy the following code into it. You can either create the file using one of your preferred command line editors (nano, vim, emacs).
```

from google.cloud import storage, language, bigquery

# Set up your GCS, NL, and BigQuery clients

storage_client = storage.Client()
nl_client = language.LanguageServiceClient()
bq_client = bigquery.Client(project='Project ID')

dataset_ref = bq_client.dataset('news_classification_dataset')
dataset = bigquery.Dataset(dataset_ref)
table_ref = dataset.table('article_data')
table = bq_client.get_table(table_ref)

# Send article text to the NL API's classifyText method

def classify_text(article):
    response = nl_client.classify_text(
        document=language.Document(
            content=article,
            type=language.Document.Type.PLAIN_TEXT
        )
    )
    return response

rows_for_bq = []
files = storage_client.bucket('qwiklabs-test-bucket-gsp063').list_blobs()
print("Got article files from GCS, sending them to the NL API (this will take ~2 minutes)...")

# Send files to the NL API and save the result to send to BigQuery

for file in files:
    if file.name.endswith('txt'):
        article_text = file.download_as_bytes().decode('utf-8')  # Decode bytes to string
        nl_response = classify_text(article_text)
        if len(nl_response.categories) > 0:
            rows_for_bq.append((article_text, nl_response.categories[0].name, nl_response.categories[0].confidence))

print("Writing NL API article data to BigQuery...")

# Write article text + category data to BQ

if rows_for_bq:
    errors = bq_client.insert_rows(table, rows_for_bq)
    if errors:
        print("Encountered errors while writing to BigQuery:", errors)
else:
    print("No articles found in the specified bucket.")
```
5. Run the following script:
```python3 classify-text.py```
![Python](../screenshots/03_Python_classify.png)

6. In BigQuery, navigate to the article_data table in the Explorer tab and click Query to query the table:
![articlequery](../screenshots/03_article_data.png)


---

## 🔹 Task 7. Analyze categorized news data in BigQuery

First, see which categories were most common in the dataset.

1. In the BigQuery console, click + SQL query.

2. Enter the following query:
```
SELECT
  category,
  COUNT(*) c
FROM
  `Project ID.news_classification_dataset.article_data`
GROUP BY
  category
ORDER BY
  c DESC
```
3. Now click Run.

![Result1](../screenshots/03_Result_query.png)



✅ Lab Completed