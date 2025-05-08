
Creating an NBA Data Lake for Analytics Using AWS Services

# NBADataLake

This repository contains the `setup_nba_data_lake.py` script, which automates the creation of a data lake for NBA analytics using AWS services. The script integrates Amazon S3, AWS Glue, and Amazon Athena, and sets up the infrastructure needed to store and query NBA-related data.

---

## Overview

The `setup_nba_data_lake.py` script performs the following actions:

- Creates an Amazon S3 bucket to store raw and processed data.
- Uploads sample NBA data (JSON format) to the S3 bucket.
- Creates an AWS Glue database and an external table for querying the data.
- Configures Amazon Athena for querying data stored in the S3 bucket.

---

## Prerequisites

### **API Access**

1. Create a free account at [Sportsdata.io](https://sportsdata.io).
2. Navigate to **Developers → API Resources → Introduction & Testing**.
3. Register for "SportsDataIO API Free Trial" (select NBA).
4. Access the Developer Portal via the email confirmation link.
5. Select NBA from the left navigation panel.
6. Locate the "Standings" section and find your API key under "Query String Parameters".
7. Save this API key for script configuration.

### **AWS Permissions**

Your IAM user/role must have the following permissions:

#### **Amazon S3**

- `s3:CreateBucket`
- `s3:PutObject`
- `s3:DeleteBucket`
- `s3:ListBucket`

#### **AWS Glue**

- `glue:CreateDatabase`
- `glue:CreateTable`
- `glue:DeleteDatabase`
- `glue:DeleteTable`

#### **Amazon Athena**

- `athena:StartQueryExecution`
- `athena:GetQueryResults`

---

## Setup Instructions

### **Step 1: Access Your AWS Account**

- Sign into your AWS Console and launch the AWS CloudShell (no additional authentication required).
- OR authenticate into your AWS account from any terminal with AWS CLI installed (authentication required: credentials, roles, etc.).

### **Step 2: Create the **``** File**

1. In the CLI, type:
   ```bash
   nano setup_nba_data_lake.py
   ```
   OR
   ```bash
   vi setup_nba_data_lake.py
   ```
2. Copy the contents of the `setup_nba_data_lake.py` file from the repository.
3. Paste the contents into the editor.
4. Find the line under `# Sportsdata.io configurations` that says `api_key` and paste your API key inside the quotation marks.
5. Save the file and exit:
   - Press `Ctrl + X` to exit, `Y` to save the file, and `Enter` to confirm the file name.

### **Step 3: Create the **``** File**

1. In the CLI, type:
   ```bash
   nano .env
   ```
2. Paste the following lines of code into the file (replace `your_sportsdata_api_key` with your actual API key):
   ```plaintext
   SPORTS_DATA_API_KEY=your_sportsdata_api_key
   NBA_ENDPOINT=https://api.sportsdata.io/v3/nba/scores/json/Players
   ```
3. Save the file and exit.

### **Step 4: Run the Script**

1. Execute the script:
   ```bash
   python3 setup_nba_data_lake.py
   ```
2. You should see messages confirming the successful creation of resources, upload of sample data, and the completion of the data lake setup.

### **Step 5: Verify the Resources**

#### **Amazon S3**

1. In the AWS Management Console, search for **S3** and click on the relevant bucket name (e.g., `Sports-analytics-data-lake-container`).
2. Verify the presence of the following folders:
   - `raw-data` (contains `nba_player_data.json`).

#### **Amazon Athena**

1. Navigate to Amazon Athena in the AWS Console.
2. Run the following query:
   ```sql
   SELECT FirstName, LastName, Position, Team
   FROM nba_players
   WHERE Position = 'PG';
   ```
3. Verify the output under the **Query Results** section.

---

## Cleanup

To delete all resources created by the script, use the `delete_resources.py` script. This script will:

- Remove the S3 bucket and its contents.
- Delete the AWS Glue database and tables.
- Clear Athena configurations.

Run the cleanup script as follows:

```bash
python3 delete_resources.py
```

---

## Key Learnings

- Securing AWS services with least privilege IAM policies.
- Automating the creation of cloud services with Python scripts.
- Integrating external APIs into cloud workflows.

---


