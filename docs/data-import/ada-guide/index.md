---
layout: default
parent: Data import
title: ADA file upload guide
description: Step-by-step guide on uploading CSV files through ADA for analysis. Includes file requirements, error resolutions, and troubleshooting tips.
nav_order: 2
---

# CSV Upload Workflow Documentation

## Introduction

This document outlines the workflow for uploading CSV files into our system through **ADA for
BoostKPI**. By following these steps, users can efficiently prepare and upload data for in-depth
analysis, leveraging Ada's integration with our system.

## CSV upload

### Step 1: Opening "ADA for BoostKPI"

Access ADA through platform's chat interface. Initiate the CSV upload process by asking ADA for CSV
analysis while providing the file to ADA.

### Step 2: Uploading and Analyzing the CSV File

1. ADA analyzes the CSV file, identifying the time column, dimension columns, and metric columns.
2. A summary of the file's structure will be provided to you.
3. You will be asked to validate the columns before proceeding to the BoostKPI file upload step.

![Uploading CSV file to ADA](/images/ada/ada-file-upload.png)

### Step 3: Fetching Redirect Link

1. ADA will request a redirect link from our API, using the column information from your CSV file.
2. You will receive a link that redirects you to the Upload page, where you can complete the final
   upload step that enables in-depth analysis functionality.

   <video autoplay="autoplay" loop="loop" width="768" height="512" muted>
     <source src="/images/ada/ada_upload_page.webm" type="video/webm">
   </video>

**Note:** The final step involves uploading the analyzed CSV file on the Upload page. Upon
successful upload, the system will load the file into our data warehouse, and you will be instructed
to return to ADA for confirmation.

## CSV File Requirements

- **Date/TimeStamp Column:** The file must contain at least one date or timestamp column.
- **Dimension Columns:** At least one dimension column is required.
- **Metric Columns:** The file must include at least one metric column.
- **File Size Limit:** The CSV file must not exceed 1 million rows.

### Example of a valid CSV Structure

```csv
Date,Dimension1,Metric1
2023-01-01,ExampleDimension,100
2023-01-01,ExampleDimension2,0.1
```

## Troubleshooting

When errors occur during the CSV upload process, the Upload page will provide specific messages
based on the issue encountered. Below are common errors and their resolutions:

- **"Invalid temporal column format. Try formatting dates as yyyy-MM-dd and timestamps as yyyy-MM-dd
  HH:mm:ss"**:
    - Ensure your date and timestamp columns follow the correct format.
- **"KPI columns must contain numeric data"**:
    - Check that your metric columns contain only non-negative numbers.
- **"Column names must only use the characters a-z, A-Z, 0-9, and _."**:
    - Verify that your column names adhere to the specified character set.
- **"Unable to parse CSV file. Please use comma delimiters."**:
    - Ensure your CSV is formatted with commas as the delimiter.
- **"Unable to upload, please contact BoostKPI"**
    - Indicates a general issue with the upload process. Please verify your file format and try
      again. If the issue persists, contact support.

For other issues or if you need further assistance, please contact our support team.

## FAQs 

**Q: What if my CSV file exceeds the 1 million row limit?**

A: Consider providing only part of the file that contains data required for the analysis.

**Q: How can I ensure my date and timestamp columns are correctly formatted?**

A: Use the format `yyyy-MM-dd` for dates and `yyyy-MM-dd HH:mm:ss` for timestamps, ensuring consistency
across your file.

## Contact Support

If you encounter issues not covered in this documentation, please reach out to our support team at
<a href="mailto:contact@boostkpi.com">contact@boostkpi.com</a> for assistance.