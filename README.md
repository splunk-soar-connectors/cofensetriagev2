# Cofense Triage v2 API

Publisher: Cofense \
Connector Version: 1.1.0 \
Product Vendor: Cofense \
Product Name: Triage v2 \
Minimum Product Version: 6.0.0

This app supports actions for Cofense Triage's version 2 API for faster bidirectional phishing analysis and response

## Explanation of the Asset Configuration Parameters

The asset configuration parameters affect [test connectivity] and some other actions of the
application. Below are the explanation and usage of all these parameters. The parameters related to
test connectivity action are Server URL, Verify server certificate, Client ID, and Client Secret.

- **Server URL:** The URL used to connect with the Cofense Triage server. Example:
  https://platform.cofensetriage.com
- **Verify server certificate:** Validate server certificate.
- **Client ID:** Client ID.
- **Client Secret:** Client Secret.
- **Data to be ingested:** The type of data that is to be ingested. The following are the valid
  values:
  - reports
  - threat_indicators
- **Threat indicator type:** The type of threat indicators to retrieve. The default value is "All"
  which retrieves all types of threat indicators. The following are the valid values that the
  parameter can take:
  - All
  - Header
  - Hostname
  - URL
  - MD5
  - SHA256
- **Threat indicator level:** The level of the threat indicators to retrieve. The default value is
  "All" which retrieves all levels of threat indicators. The following are the valid values that
  the parameter can take:
  - All
  - Malicious
  - Suspicious
  - Benign
- **Report location:** The location of the reports to retrieve. The default value is "All" which
  retrieves reports from all the locations. The following are the valid values that the parameter
  can take:
  - All
  - Inbox
  - Reconnaissance
  - Processed
- **Match priority:** The highest priority of a rule matching the reported email.
- **Category ID:** The category ID of the report.
- **Tags:** This parameter allows filtering the reports based on the list of comma-separated tags.
  If the tag value contains a comma, enclose it in double-quotes, for example:
  tag1,"test,tag",tag2. If a comma-separated list is provided, reports matching any of the tags
  from the provided list will be retrieved.
- **Categorization tags:** This parameter allows filtering the reports based on the list of
  comma-separated categorization tags. If a comma-separated list is provided, reports matching any
  of the tags from the provided list will be retrieved.
- **Ingest subfields:** Whether or not to ingest the subfields of the selected data. If this
  parameter is set to true, the data and all the resources related to the data that are present in
  the relationships will be ingested.
- **Category ID to severity mapping:** The mapping in JSON format between the category ID of the
  report and the Phantom container severity. If no value is provided, then the default mapping
  will be used and, if the category ID isn't present in the default mapping the severity will be
  set to "Low". If a value is provided, the combination of the provided value and the default
  mapping will be used to decide the severity. The default mapping is: {"High": ["4"], "Medium":
  ["3"], "Low": ["1", "2", "5"]}. Example value for the parameter is: {"High": ["8", "9"],
  "Medium": ["7"], "Low": ["6"]}
- **Cef mapping:** This parameter is a JSON dictionary represented as a serialized JSON string.
  Each key in the dictionary is a potential key name in an artifact that is to be renamed to the
  value. For example, if the cef_mapping is {"website":"requestURL"} your artifact will have
  requestURL cef field in place of website cef field. This parameter will be taken into
  consideration only during ingestion.
- **Start date:** The initial start date and time of the ingestion. This parameter retrieves the
  data that was updated on or after the provided date. It will be taken into consideration during
  the poll now and the first run of scheduled/interval polling.
- **Sort:** This parameter allows sorting the data based on the 'updated_at' date. The default
  value is "oldest_first" which sorts the results in the oldest first order. The following are the
  valid values that the parameter can take:
  - oldest_first
  - latest_first
- **Update state after:** This parameter saves the context after ingestion of every provided
  number of containers. This parameter is only used for scheduled/interval polling and only if the
  sort parameter value is "oldest_first".
- **Max results:** Maximum number of results to ingest. If not provided all the data will be
  ingested.

## Explanation of the Actions' Parameters

- ### Test Connectivity (Action Workflow Details)

  - This action will test the connectivity of the Phantom server to the Cofense Triage instance
    by making an initial API call using the provided asset configuration parameters. This action
    can be used to generate a new token.
  - The action validates the provided asset configuration parameters. Based on the API call
    response, the appropriate success and failure message will be displayed when the action gets
    executed.

- ### Get reports

  - **<u>Action Parameter:</u> Location**

    - This parameter allows filtering the reports based on the location. The following are the
      valid values that the parameter can take:
      - All
      - Inbox
      - Reconnaissance
      - Processed

  - **<u>Action Parameter:</u> From address**

    - This parameter allows filtering the reports based on the sender's email address of the
      reported email.

  - **<u>Action Parameter:</u> Reporter's email**

    - This parameter allows filtering the reports based on the reporter's email address of the
      reported email.

  - **<u>Action Parameter:</u> Subject**

    - This parameter allows filtering the reports with the subject containing a specific
      string. All the reports containing the provided value in the subject will be retrieved.

  - **<u>Action Parameter:</u> Match priority**

    - This parameter allows filtering the reports based on the highest priority of a rule
      matching the reported email.

  - **<u>Action Parameter:</u> Category ID**

    - This parameter allows filtering the reports based on the category ID of the report.

  - **<u>Action Parameter:</u> Start date**

    - This parameter allows filtering the reports updated on or after the provided date.

  - **<u>Action Parameter:</u> End date**

    - This parameter allows filtering the reports updated before the provided date.

  - **<u>Action Parameter:</u> Tags**

    - This parameter allows filtering the reports based on the list of comma-separated tags.
      If the tag value contains a comma, enclose it in double-quotes, for example:
      tag1,"test,tag",tag2. If a comma-separated list is provided, reports matching any of the
      tags from the provided list will be retrieved.

  - **<u>Action Parameter:</u> Categorization tags**

    - This parameter allows filtering the reports based on the list of comma-separated
      categorization tags. If a comma-separated list is provided, reports matching any of the
      tags from the provided list will be retrieved.

  - **<u>Action Parameter:</u> Sort**

    - This parameter allows sorting the reports based on the 'updated_at' date of the report.
      By default, it will sort in the oldest first order. The following are the valid values
      that the parameter can take:
      - oldest_first
      - latest_first

  - **<u>Action Parameter:</u> Ingest report**

    - This parameter allows the ingestion of the report into the container.

  - **<u>Action Parameter:</u> Ingest subfields**

    - This parameter allows the ingestion of the fields relating to the report into the
      container. If this parameter is set to true, the report and all the resources related to
      the report that are present in the relationships together will get ingested into the
      container.

  - **<u>Action Parameter:</u> Label**

    - This parameter allows the ingestion of data into the container(s) with the provided
      label. The label must be valid or the action will fail. Required if 'ingest_report' or
      'ingest_subfields' is set. This parameter will be taken into consideration only during
      ingestion.

  - **<u>Action Parameter:</u> Tenant**

    - This parameter allows the creation of container(s) for the provided tenant ID or tenant
      name. The tenant must be valid or the action will fail. Required if 'ingest_report' or
      'ingest_subfields' is set. This parameter will be taken into consideration only during
      ingestion.

  - **<u>Action Parameter:</u> Cef mapping**

    - This parameter is a JSON dictionary represented as a serialized JSON string. Each key in
      the dictionary is a potential key name in an artifact that is to be renamed to the
      value. For example, if the cef_mapping is {"website":"requestURL"} your artifact will
      have requestURL cef field in place of website cef field. This parameter will be taken
      into consideration only during ingestion.

  - **<u>Action Parameter:</u> Max results**

    - Maximum number of results to return. If not provided all the data will be retrieved.

  - **Note -** If no value is provided in any parameter, then all the records will be retrieved.

  - **Example:**

    - List all the reports present in Inbox containing “demo” word in the subject and having
      match priority equals 5 and is sent by 'abc@test.com'.
      - Location = Inbox
      - Subject = Demo
      - Match Priority = 5
      - From Address = abc@test.com
    - List all the reports updated between 2020-09-23T08:31:58Z and 2020-09-29T09:00:00Z and
      sort them in oldest_first order.
      - Start date = 2020-09-23T08:31:58Z
      - End date = 2020-09-29T09:00:00Z
      - Sort = oldest_first
    - List the reports in the latest_first order.
      - Sort = latest_first

- ### Get report

  - **<u>Action Parameter:</u> Report ID**

    - The ID of the report to be retrieved.

  - **<u>Action Parameter:</u> Ingest report**

    - This parameter allows the ingestion of the report into the container.

  - **<u>Action Parameter:</u> Ingest subfields**

    - This parameter allows the ingestion of the fields relating to the report into the
      container. If this parameter is set to true, the report and all the resources related to
      the report that are present in the relationships together will get ingested into the
      container.

  - **<u>Action Parameter:</u> Label**

    - This parameter allows the ingestion of data into the container(s) with the provided
      label. The label must be valid or the action will fail. Required if 'ingest_report' or
      'ingest_subfields' is set. This parameter will be taken into consideration only during
      ingestion.

  - **<u>Action Parameter:</u> Tenant**

    - This parameter allows the creation of container(s) for the provided tenant ID or tenant
      name. The tenant must be valid or the action will fail. Required if 'ingest_report' or
      'ingest_subfields' is set. This parameter will be taken into consideration only during
      ingestion.

  - **<u>Action Parameter:</u> Cef mapping**

    - This parameter is a JSON dictionary represented as a serialized JSON string. Each key in
      the dictionary is a potential key name in an artifact that is to be renamed to the
      value. For example, if the cef_mapping is {"website":"requestURL"} your artifact will
      have requestURL cef field in place of website cef field. This parameter will be taken
      into consideration only during ingestion.

  - **Example:**

    - Fetch the report with ID equals 15.
      - Report ID = 15

- ### Categorize report

  - **<u>Action Parameter:</u> Report ID**

    - This parameter is the ID of the report which the user wants to categorize.

  - **<u>Action Parameter:</u> Category ID**

    - This parameter is the ID of the category into which the user wants to categorize the
      report. Category ID is either known by Cofense Triage users or it can be fetched from
      the output of Get categories action.

  - **<u>Action Parameter:</u> Category Name**

    - This parameter is the name of the category into which the user wants to categorize the
      report. This parameter can be provided if the category ID is not known by Cofense Triage
      users.

  - **<u>Action Parameter:</u> Response ID**

    - This parameter is the ID of the response.

  - **<u>Action Parameter:</u> Categorization Tags**

    - This parameter allows the user to provide multiple tags to be given to the report while
      categorizing it. It accepts a comma-separated list of tags.

  - **Note -** If both category ID and category name are provided, then category ID will be
    given a higher priority.

  - **Example:**

    - Categorize the report having Report ID 5, with given category ID 1, and add
      categorization tag ‘test’.
      - Report ID = 5
      - Category ID = 1
      - Categorization tags = test
    - Categorize the report having Report ID 10, with given category ID 2 and add
      categorization tag ‘test tag’, also send a response using response template ID 2.
      - Report ID = 10
      - Category ID = 2
      - Categorization tags = test tag
      - Response ID = 2

- ### Get reporters

  - **<u>Action Parameter:</u> VIP**

    - This parameter allows searching for the VIP reporters. If the value of the parameter is
      false, then all the reporters will be retrieved.

  - **<u>Action Parameter:</u> Reputation score**

    - This parameter allows searching for reporters having the provided reputation score. It
      allows a comma-separated list. If a comma-separated list is provided, then the reporters
      with any of the specified scores will be retrieved.

  - **<u>Action Parameter:</u> Email**

    - This parameter allows searching for the reporter with a specific email.

  - **<u>Action Parameter:</u> Sort**

    - This parameter allows sorting the reporters based on the ID. By default, it will sort in
      the oldest first order. The following are the valid values that the parameter can
      take:
      - oldest_first
      - latest_first

  - **<u>Action Parameter:</u> Max results**

    - Maximum number of results to return. If not provided, all the data will be retrieved.

  - **Note -** If no value is provided in any parameter, then all the records will be retrieved.

  - **Example:**

    - List the latest 15 VIP reporters with a reputation score equals 15.
      - VIP = true
      - Reputation Score = 15
      - Max results = 15
      - Sort = latest_first
    - Fetch the reporter with the email address abc@test.com.
      - Email = abc@test.com

- ### Get reporter

  - **<u>Action Parameter:</u> Reporter ID**

    - This parameter is the ID of the reporter to fetch.

  - **Example:**

    - Fetch the reporter with the Reporter ID equals 10.
      - Report ID = 10

- ### Get URLs

  - **<u>Action Parameter:</u> Risk score**

    - This parameter is the risk score of the URL.

  - **<u>Action Parameter:</u> Risk score operator**

    - This parameter is the operator to work with the risk score parameter. The default value
      is 'eq'.For example: if the risk score = 5 and the risk score operator = 'lt', then all
      the URLs having a risk score less than 5 will be retrieved. The following are the valid
      values that the parameter can take:
      - eq
      - not_eq
      - lt
      - lteq
      - gt
      - gteq

  - **<u>Action Parameter:</u> URL Value**

    - This parameter is the value of the URL to search for.

  - **<u>Action Parameter:</u> Start date**

    - This parameter allows filtering the URLs updated on or after the provided date.

  - **<u>Action Parameter:</u> End date**

    - This parameter allows filtering the URLs updated before the provided date.

  - **<u>Action Parameter:</u> Sort**

    - This parameter allows sorting the URLs based on the 'updated_at' date of the URL. By
      default, it will sort in the oldest first order. The following are the valid values that
      the parameter can take:
      - oldest_first
      - latest_first

  - **<u>Action Parameter:</u> Max results**

    - Maximum number of results to return. If not provided, all the data will be retrieved.

  - **Note -** If no value is provided in any parameter, then all the records will be retrieved.

  - **Example:**

    - List all the URLs having a risk score equals 5 in the latest first order.
      - Risk score ID = 5
      - Risk score operator = eq
      - Sort = latest_first
    - List the URL having value equals 'https://testurl.com'.
      - URL value = https://testurl.com
    - List oldest 5 URLs that are updated between 2020-09-23T08:31:58Z and
      2020-09-29T09:00:00Z.
      - Start date = 2020-09-23T08:31:58Z
      - End date = 2020-09-29T09:00:00Z
      - Sort = oldest_first
      - Max results = 5

- ### Get url

  - **<u>Action Parameter:</u> URL ID**

    - This parameter is the ID of the URL to fetch.

  - **Example:**

    - Fetch the URL with URL ID equals 5.
      - URL ID = 5

- ### Create response

  - **<u>Action Parameter:</u> Name**

    - This parameter specifies a short display name of the response sent to individuals when a
      report is categorized.

  - **<u>Action Parameter:</u> Description**

    - This parameter specifies the expanded name or description of the response.

  - **<u>Action Parameter:</u> Subject**

    - This parameter specifies the subject of the response. It supports template variables.

  - **<u>Action Parameter:</u> Body**

    - This parameter specifies the body of the email. It supports template variables.

  - **<u>Action Parameter:</u> To reporter**

    - This parameter specifies whether to add the reporter to the response recipient list
      (true) or not (false). The default is true. Either 'to_reporter' or 'to_other', or both,
      must be enabled.

  - **<u>Action Parameter:</u> To other**

    - This parameter specifies whether to add the addresses specified in 'to_other_address' to
      the response recipient list (true) or not (false). The default is false. If true,
      specify one or more values in 'to_other_address'. Either to_reporter or 'to_other', or
      both, must be enabled.

  - **<u>Action Parameter:</u> To other address**

    - This parameter is a comma-separated list of email addresses to send the response to.
      Works with 'to_other'.

  - **<u>Action Parameter:</u> Attach original**

    - This parameter specifies whether to attach the original email to the response (true) or
      not (false).

  - **<u>Action Parameter:</u> CC address**

    - This parameter is a comma-separated list of email addresses to CC the response to.

  - **<u>Action Parameter:</u> BCC address**

    - This parameter is a comma-separated list of email addresses to BCC the response to.

  - **Template variables:** The user can insert variables into the subject and body of the
    response while creating it. When the response is sent as a result of categorizing a report,
    Cofense Triage replaces the variables with information from that report. The following are
    the template variables

    - \[SUBJECT\]: Replaced with the subject of the reported email.
    - \[REPORT_DATE\]: Replaced with the date the email was reported.

  - **Example:**

    - Create a response with name: "Example Response", Description: "This is an example
      response", Subject: "Email '[SUBJECT]' reported [REPORT_DATE] is SAFE", and Body =
      "The email '[SUBJECT]' that you reported on [REPORT_DATE] is safe".
      - Name = Example Response
      - Description = This is an example response
      - Subject = Email '[SUBJECT]' reported [REPORT_DATE] is SAFE
      - Body = The email '[SUBJECT]' that you reported on [REPORT_DATE] is safe
    - Create a response with name: "Example Response", Subject: "Email '[SUBJECT]' reported
      [REPORT_DATE] is SAFE", and Body = "The email '[SUBJECT]' that you reported on
      [REPORT_DATE] is safe". The response should be sent to the reporter and not others.
      - Name = Example Response
      - To reporter = true
      - To other = false
      - Subject = Email '[SUBJECT]' reported [REPORT_DATE] is SAFE
      - Body = The email '[SUBJECT]' that you reported on [REPORT_DATE] is safe

  **Note:** This action is supported for Cofense Triage with version older than 1.23.

- ### Get responses

  - **<u>Action Parameter:</u> Max results**

    - This parameter allows the user to limit the number of results. It expects a numeric
      value as an input.

  - **Example:**

    - List 50 responses.
      - Max results = 50

  **Note:** This action is supported for Cofense Triage with version older than 1.23.

- ### Create threat indicator

  - **<u>Action Parameter:</u> Level**

    - This parameter is the level of threat indicator. The following are the valid values that
      the parameter can take:
      - Malicious
      - Suspicious
      - Benign

  - **<u>Action Parameter:</u> Type**

    - This parameter is the type of threat indicator. The following are the valid values that
      the parameter can take:
      - Header
      - Hostname
      - URL
      - MD5
      - SHA256

  - **<u>Action Parameter:</u> Value**

    - This parameter is the value of the threat indicator. If the value of the parameter
      'type' is 'Header', then the value of this parameter should be in the form
      {header_key}:{header_value}.

  - **<u>Action Parameter:</u> Source**

    - This parameter is the source of the threat indicator. The default value of this
      parameter is "Splunk_Phantom-UI"

  - **Example:**

    - Create a malicious threat indicator with type: URL and value: 'https://testurl.com'.
      - Level = Malicious
      - Type = URL
      - Value = 'https://testurl.com'
    - Create a Suspicious threat indicator, source: 'Splunk_Phantom-UI', type: Header and
      value: 'From:test@test.com'
      - Level = Suspicious
      - Type = Header
      - Value = From:test@test.com
      - Source = Splunk_Phantom-UI

- ### Get categories

  - **<u>Action Parameter:</u> Name**

    - This parameter allows the user to fetch the categories with the name containing a
      specific string.

  - **<u>Action Parameter:</u> Malicious**

    - This parameter allows the user to fetch the categories based on whether the category is
      used to classify malicious reports or not. If the value is false, then all the
      categories will be fetched.

  - **<u>Action Parameter:</u> Max results**

    - Maximum number of results to return. If not provided, all the data will be retrieved.

  - **Note -** If no value is provided in any parameter, then all the records will be retrieved.

  - **Example:**

    - List the categories containing ‘threat’ in the name and are malicious.
      - Name = Threat
      - Malicious = true
    - List 50 categories.
      - Max results = 50

- ### Get threat indicators

  - **<u>Action Parameter:</u> Level**

    - This parameter allows filtering based on the level of threat indicator. The following
      are the valid values that the parameter can take:
      - All
      - Malicious
      - Suspicious
      - Benign

  - **<u>Action Parameter:</u> Type**

    - This parameter allows filtering based on the type of threat indicator. The following are
      the valid values that the parameter can take:
      - All
      - Header
      - Hostname
      - URL
      - MD5
      - SHA256

  - **<u>Action Parameter:</u> Source**

    - This parameter allows filtering based on the source of the threat. If not provided,
      threat indicators from all the sources will be fetched.

  - **<u>Action Parameter:</u> Value**

    - This parameter allows filtering based on the actual value of the threat indicator.

  - **<u>Action Parameter:</u> Start date**

    - This parameter allows the user to fetch the threat indicators updated on or after the
      provided date.

  - **<u>Action Parameter:</u> End date**

    - This parameter allows the user to fetch the threat indicators updated before the
      provided date.

  - **<u>Action Parameter:</u> Sort**

    - This parameter allows sorting the result data set based on the 'updated_at' date of the
      threat indicator. By default, it will sort in the oldest first order. The following are
      the valid values that the parameter can take:
      - oldest_first
      - latest_first

  - **<u>Action Parameter:</u> Ingest threat indicator**

    - This parameter allows ingestion of the threat indicator(s) into the container(s).

  - **<u>Action Parameter:</u> Ingest subfields**

    - This parameter allows the ingestion of the fields relating to the threat indicator into
      the container. If this parameter is set to true, the threat indicator and all the
      resources related to the threat indicator that are present in the relationships together
      will get ingested.

  - **<u>Action Parameter:</u> Label**

    - This parameter allows the ingestion of data into the container(s) with the provided
      label. The label must be valid or the action will fail. Required if
      'ingest_threat_indicator' or 'ingest_subfields' is set. This parameter will be taken
      into consideration only during ingestion.

  - **<u>Action Parameter:</u> Tenant**

    - This parameter allows the creation of container(s) for the provided tenant ID or tenant
      name. The tenant must be valid or the action will fail. Required if
      'ingest_threat_indicator' or 'ingest_subfields' is set. This parameter will be taken
      into consideration only during ingestion.

  - **<u>Action Parameter:</u> Cef mapping**

    - This parameter is a JSON dictionary represented as a serialized JSON string. Each key in
      the dictionary is a potential key name in an artifact that is to be renamed to the
      value. For example, if the cef_mapping is {"website":"requestURL"} your artifact will
      have requestURL cef field in place of website cef field. This parameter will be taken
      into consideration only during ingestion.

  - **<u>Action Parameter:</u> Max results**

    - Maximum number of results to return. If not provided all the data will be retrieved.

  - **Note -** If no value is provided in any parameter then all the records will be retrieved.

  - **Example:**

    - List all the Malicious threat indicators that are URLs and are reported from the
      Triage-UI source.
      - Level = Malicious
      - Type = URL
      - Source = Triage-UI
    - List all the threat indicators updated between 2020-09-23T08:31:58Z and
      2020-09-29T09:00:00Z and sort them in oldest_first order.
      - Start date = 2020-09-23T08:31:58Z
      - End date = 2020-09-29T09:00:00Z
      - Sort = oldest_first
    - List 50 threat indicators in the latest first order.
      - Max results = 50
      - Sort = latest_first

- ### Get email

  - **<u>Action Parameter:</u> Report ID**

    - This parameter is the ID of the report.

  - **<u>Action Parameter:</u> Download method**

    - This parameter allows the user to download the email as an artifact or as a vaulted
      file.

  - **<u>Action Parameter:</u> Create vaulted file artifact**

    - If storing the file as a vaulted file, this parameter allows the user to create an
      artifact referencing that file.

  - **Example:**

    - Download email for report ID equals 10.
      - Report ID = 10
      - Download method = vaulted file

- ### Get Comments

  - **<u>Action Parameter:</u> Body format**

    - This parameter allows filtering the comments based on the body format. The following are
      the valid values that the parameter can take:
      - all
      - text
      - json

  - **<u>Action Parameter:</u> Tags**

    - This parameter allows filtering the comments based on the list of comma-separated tags.
      If the tag value contains a comma, enclose it in double-quotes, for example:
      tag1,"test,tag",tag2. If a comma-separated list is provided, comments matching any of
      the tags from the provided list will be retrieved.

  - **<u>Action Parameter:</u> Start date**

    - This parameter allows filtering the comments updated on or after the provided date.

  - **<u>Action Parameter:</u> End date**

    - This parameter allows filtering the comments updated before the provided date.

  - **<u>Action Parameter:</u> Sort**

    - This parameter allows sorting the comments based on the 'updated_at' date of the
      comment. By default, it will sort in the oldest first order. The following are the valid
      values that the parameter can take:
      - oldest_first
      - latest_first

  - **<u>Action Parameter:</u> Max results**

    - Maximum number of results to return. If not provided, all the data will be retrieved.

  - **Note -** If no value is provided in any parameter, then all the records will be retrieved.

  - **Example:**

    - List the latest 20 comments having 'text' body format with a tag 'test'.
      - Body format = text
      - Tags = test
      - Sort = latest_first
      - Max results = 20
    - List all the comments updated between 2020-09-23T08:31:58Z and 2020-09-29T09:00:00Z and
      sort them in oldest_first order.
      - Start date = 2020-09-23T08:31:58Z
      - End date = 2020-09-29T09:00:00Z
      - Sort = oldest_first
    - List the comments in the latest_first order.
      - Sort = latest_first

- ### Get comment

  - **<u>Action Parameter:</u> Comment ID**

    - This parameter is the ID of the comment to fetch.

  - **Example:**

    - Fetch the comment with comment ID equals 5.
      - Comment ID = 5

- ### Get rule

  - **<u>Action Parameter:</u> Rule ID**

    - This parameter is the ID of the rule to fetch.

  - **<u>Action Parameter:</u> Ingest report**

    - This parameter allows ingestion of reports related to the rule.

  - **<u>Action Parameter:</u> Ingest subfields**

    - This parameter allows the ingestion of the fields relating to the report into the
      container. If this parameter is set to true, the report and all the resources related to
      the report that are present in the relationships together will get ingested into the
      container.

  - **<u>Action Parameter:</u> Label**

    - This parameter allows the ingestion of data into the container(s) with the provided
      label. The label must be valid or the action will fail. Required if 'ingest_report' or
      'ingest_subfields' is set. This parameter will be taken into consideration only during
      ingestion.

  - **<u>Action Parameter:</u> Tenant**

    - This parameter allows the creation of container(s) for the provided tenant ID or tenant
      name. The tenant must be valid or the action will fail. Required if 'ingest_report' or
      'ingest_subfields' is set. This parameter will be taken into consideration only during
      ingestion.

  - **<u>Action Parameter:</u> Cef mapping**

    - This parameter is a JSON dictionary represented as a serialized JSON string. Each key in
      the dictionary is a potential key name in an artifact that is to be renamed to the
      value. For example, if the cef_mapping is {"website":"requestURL"} your artifact will
      have requestURL cef field in place of website cef field. This parameter will be taken
      into consideration only during ingestion.

  - **Example:**

    - Fetch the rule with rule ID equals 5 and ingest the reports related to the rule.
      - Rule ID = 5
      - Ingest reports = True
      - Label = events
      - Tenant = Default

- ### Get rules

  - **<u>Action Parameter:</u> Name**

    - This parameter allows filtering the rules with rule name containing a specific string.
      All the rules containing the provided value in the name will be retrieved.

  - **<u>Action Parameter:</u> Description**

    - This parameter allows filtering the rules with rule description containing a specific
      string. All the rules containing the provided value in the description will be
      retrieved.

  - **<u>Action Parameter:</u> Priority**

    - This parameter allows filtering the rules based on the priority.

  - **<u>Action Parameter:</u> Tags**

    - This parameter allows filtering the rules based on the list of comma-separated tags. If
      the tag value contains a comma, enclose it in double-quotes, for example:
      tag1,"test,tag",tag2. If a comma-separated list is provided, rules matching any of the
      tags from the provided list will be retrieved.

  - **<u>Action Parameter:</u> Scope**

    - This parameter allows filtering the rules based on the scope.

  - **<u>Action Parameter:</u> Author name**

    - This parameter allows filtering the rules with author name containing a specific string.
      All the rules containing the provided value in the author's name will be retrieved.

  - **<u>Action Parameter:</u> Rule context**

    - This parameter allows filtering the rules based on the context. The following are the
      valid values that the parameter can take:
      - All
      - Internal safe
      - Unwanted
      - Threat hunting
      - Phishing tactic
      - Cleanup
      - Unknown

  - **<u>Action Parameter:</u> Active**

    - This parameter allows filtering the rules based on the status. If the value of the
      parameter is false, then all the rules will be retrieved.

  - **<u>Action Parameter:</u> Reports count**

    - This parameter allows filtering the rules based on the number of reports the rule
      matched.

  - **<u>Action Parameter:</u> Reports count operator**

    - This parameter is the operator to work with the reports count parameter. The default
      value is 'eq'. For example: if the reports count = 5 and the reports count operator =
      'lt', then all the rules having a report count less than 5 will be retrieved. The
      following are the valid values that the parameter can take:
      - eq
      - not_eq
      - lt
      - lteq
      - gt
      - gteq

  - **<u>Action Parameter:</u> Start date**

    - This parameter allows filtering the rules updated on or after the provided date.

  - **<u>Action Parameter:</u> End date**

    - This parameter allows filtering the rules updated before the provided date.

  - **<u>Action Parameter:</u> Sort**

    - This parameter allows sorting the rules based on the 'updated_at' date. By default, it
      will sort in the oldest first order. The following are the valid values that the
      parameter can take:
      - oldest_first
      - latest_first

  - **<u>Action Parameter:</u> Max results**

    - Maximum number of results to return. If not provided all the data will be retrieved.

  - **Note -** If no value is provided in any parameter, then all the records will be retrieved.

  - **Example:**

    - Fetch the active rules created by 'author1' with name equals 'test' having tag equals
      'test' and priority equals 1.
      - Name = test
      - Priority = 1
      - Author name = author1
      - Active = True
      - Tags = test
    - List all the rules updated between 2020-09-23T08:31:58Z and 2020-09-29T09:00:00Z and
      sort them in oldest_first order.
      - Start date = 2020-09-23T08:31:58Z
      - End date = 2020-09-29T09:00:00Z
      - Sort = oldest_first
    - Fetch 20 rules with report count equals 5.
      - Reports count = 5
      - Reports count operator = eq
      - Max results = 20

- ### Get integration submissions

  - **<u>Action Parameter:</u> Type**

    - This parameter is the type of integration submission.

  - **<u>Action Parameter:</u> Value**

    - This parameter is the value of integration submission.

  - **Example:**

    - List integration submissions of type MD5 with value equals
      f033362ca459dcab56aa6b2274751d13.
      - Type = MD5
      - Value = f033362ca459dcab56aa6b2274751d13
    - List integration submissions of type URL with value equals http://test.com.
      - Type = URL
      - Value = http://test.com

- ### On Poll

  - ### What is On Poll

    - It will ingest data from the external system into the phantom server in the form of
      containers and artifacts. There are two approaches to polling which are mentioned below.

      - POLL NOW (Manual polling)

        - It will fetch the data every time as per the corresponding asset configuration
          parameters. It doesn’t store the last run context of the fetched data. The
          corresponding asset configuration parameters for the POLL NOW are
          ingestion_type, threat_indicator_type, threat_indicator_level, report_location,
          match_priority, category_id, tags, categorization_tags, ingest_subfields,
          category_id_to_severity, cef_mapping, start_date, sort and max_results.

      - Scheduled/Interval Polling

        - Scheduled Polling: The ingestion action can be triggered at every specified
          timestamp interval.
        - Interval Polling: The ingestion action can be triggered at every time range
          interval.
        - It will fetch the data every time as per the corresponding asset configuration
          parameters based on the stored context from the previous ingestion run. It
          stores the last run context of the fetched data. It starts fetching data based
          on the combination of the values of stored context for the previous ingestion
          run and the corresponding asset configuration parameters. The corresponding
          asset configuration parameters for the scheduled/interval are ingestion_type,
          threat_indicator_type, threat_indicator_level, report_location, match_priority,
          category_id, tags, categorization_tags, ingest_subfields,
          category_id_to_severity, cef_mapping, start_date, sort, update_state_after and
          max_results.

  - ### Containers and Artifacts creation

    - We have configured two types of data ingestion which you can select from the asset
      configuration parameters. Below are the two types

      - reports: It will ingest only the reports.
      - threat_indicators: It will ingest only the threat indicators.

    - Container

      - A container is a composite object that consists of one or more artifacts that can be
        automated. Containers are the top-level data structure that Playbooks operate on.
        Every container has a common header, and beneath that, the ability to store
        arbitrary less structured JSON.

    - Artifacts

      - Artifacts are objects that are associated with a Container and serve as
        corroboration or evidence related to the Container.

    - Each report or threat indicator will be ingested as an artifact in a separate container.
      Each subfield related to the report or the threat indicator will get ingested into the
      container of that report or threat indicator as a separate artifact if the
      'ingest_subfields' parameter is true. Below is the explanation based on the type of data
      for that.

      - **reports**

        For this type, one container will be created for each report.

        - Container 1:- Subject of the report

          - This container will be used to store fetched report data in the form of
            artifacts.

      - **threat indicators**

        For this type, one container will be created for each threat indicator.

        - Container 1:- Threat Indicator ID - ID

          - This container will be used to store fetched threat indicator data in the
            form of artifacts.

  - ### Stored Context

    - It is the concept of storing the context of the previous ingestion run. This concept
      will be used in the scheduled/interval polling. It will use the state file to store the
      last run context. This state file will be created for the created asset for the
      application on the phantom platform.

      - State file location:

        - For non-NRI Instances:
          /opt/phantom/local_data/app_states/7129d563-a28d-4afc-8081-f909dce54293
        - For NRI Instances:
          /home/phanru/phantomcyber/local_data/app_states/7129d563-a28d-4afc-8081-f909dce54293

      - The default format of state file: {"app_version": "1.0.0"}

  - **Example:**

    - Ingest the Malicious threat indicators that are URLs and are updated on or after
      2020-09-23T08:31:58Z.
      - Ingestion type = threat_indicators
      - Threat Indicator Level = Malicious
      - Threat Indicator Type = URL
      - Start date = 2020-09-23T08:31:58Z
    - Ingest the reports present in Inbox having match priority equals 5 and are updated on or
      after 2020-09-23T08:31:58Z.
      - Ingestion type = reports
      - Report Location = Inbox
      - Match Priority = 5
      - Start date = 2020-09-23T08:31:58Z

### Configuration variables

This table lists the configuration variables required to operate Cofense Triage v2 API. These variables are specified when configuring a Triage v2 asset in Splunk SOAR.

VARIABLE | REQUIRED | TYPE | DESCRIPTION
-------- | -------- | ---- | -----------
**base_url** | required | string | Server URL |
**verify_server_cert** | optional | boolean | Verify server certificate |
**client_id** | required | string | Client ID |
**client_secret** | required | password | Client Secret |
**ingestion_type** | optional | string | The type of data that is to be ingested |
**threat_indicator_type** | optional | string | Filters the results based on the type of the threat indicator. The default retrieves all |
**threat_indicator_level** | optional | string | Filters the results based on the level of the threat indicator. The default retrieves all |
**report_location** | optional | string | Filters the reports based on the location of the report. The default retrieves all |
**match_priority** | optional | numeric | Filters the results based on the highest priority of a rule matching the reported email |
**category_id** | optional | numeric | Filters the reports based on the category ID |
**tags** | optional | string | Allows filtering the reports based on the list of comma-separated tags |
**categorization_tags** | optional | string | Allows filtering the reports based on the list of comma-separated categorization tags |
**ingest_subfields** | optional | boolean | Allows ingestion of the fields relating to the fetched data into the container |
**category_id_to_severity** | optional | string | Mapping between report category ID and the Phantom container severity |
**cef_mapping** | optional | string | JSON dictionary represented as a serialized JSON string. Each key in the dictionary is a potential key name in an artifact that is to be renamed to the value |
**start_date** | optional | string | The initial start date and time of the ingestion |
**sort** | optional | string | Sorts the results based on the 'updated_at' date. The default sorts in the oldest first order |
**update_state_after** | optional | numeric | Allows updating the state after ingestion of a specified number of containers |
**max_results** | optional | numeric | Maximum number of results to ingest |

### Supported Actions

[test connectivity](#action-test-connectivity) - Validate the asset configuration for connectivity using supplied configuration \
[get reports](#action-get-reports) - Retrieve reports from the Cofense Triage Platform filtered based on the provided parameters \
[get report](#action-get-report) - Retrieve a report with the provided ID from the Cofense Triage Platform \
[get email](#action-get-email) - Downloads the raw email for the report that matches the specified report ID \
[get categories](#action-get-categories) - Retrieve categories from the Cofense Triage Platform filtered based on the provided parameters \
[get responses](#action-get-responses) - Retrieve responses from the Cofense Triage Platform. This action is supported for Cofense Triage with version older than 1.23 \
[create response](#action-create-response) - Create a response. This action is supported for Cofense Triage with version older than 1.23 \
[categorize report](#action-categorize-report) - Categorize a report into the provided category \
[get threat indicators](#action-get-threat-indicators) - Retrieve threat indicators from the Cofense Triage Platform filtered based on the provided parameters \
[create threat indicator](#action-create-threat-indicator) - Create a threat indicator with the provided parameters \
[get reporters](#action-get-reporters) - Retrieve reporters from the Cofense Triage Platform filtered based on the provided parameters \
[get reporter](#action-get-reporter) - Retrieve a reporter from the Cofense Triage Platform for the provided reporter ID \
[get urls](#action-get-urls) - Retrieve URLs from the Cofense Triage Platform filtered based on the provided parameters \
[get url](#action-get-url) - Retrieve a URL from the Cofense Triage Platform for the provided URL ID \
[get comments](#action-get-comments) - Retrieve comments from the Cofense Triage Platform filtered based on the provided parameters \
[get comment](#action-get-comment) - Retrieve a comment from the Cofense Triage Platform for the provided comment ID \
[get rules](#action-get-rules) - Retrieve rules from the Cofense Triage Platform filtered based on the provided parameters \
[get rule](#action-get-rule) - Retrieve a rule from the Cofense Triage Platform for the provided rule ID \
[get integration submissions](#action-get-integration-submissions) - Retrieve integration submissions from the Cofense Triage Platform filtered based on the provided parameters \
[on poll](#action-on-poll) - Action handler for the on poll ingest functionality

## action: 'test connectivity'

Validate the asset configuration for connectivity using supplied configuration

Type: **test** \
Read only: **True**

#### Action Parameters

No parameters are required for this action

#### Action Output

No Output

## action: 'get reports'

Retrieve reports from the Cofense Triage Platform filtered based on the provided parameters

Type: **investigate** \
Read only: **True**

If the 'ingest_subfields' parameter is true, the report and the subfields together will get ingested into the container. If no value is provided in any parameter, then all the records will be retrieved. If reporter_id and category_id both are provided then reports will be fetched based on category_id.

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**location** | optional | Allows filtering the reports based on the location | string | `cofensetriage report location` |
**from_address** | optional | Allows filtering the reports based on the sender's email address of the reported email | string | `email` |
**reporter_email** | optional | Allows filtering the reports based on the reporter's email address | string | `email` |
**subject** | optional | Allows filtering the reports based on the subject of the reported email | string | `cofensetriage report subject` |
**match_priority** | optional | Allows filtering the result data set based on the highest priority of a rule matching the reported email | numeric | `cofensetriage priority` |
**category_id** | optional | Allows filtering the reports based on the category ID | numeric | `cofensetriage category id` |
**start_date** | optional | Allows filtering the reports updated on or after the provided date | string | `date` |
**end_date** | optional | Allows filtering the reports updated before the provided date | string | `date` |
**tags** | optional | Allows filtering the reports based on the list of comma-separated tags. If the tag value contains a comma, enclose it in double-quotes (Example: tag1,"test,tag",tag2) | string | `cofensetriage tag` |
**categorization_tags** | optional | Allows filtering the reports based on the list of comma-separated categorization tags | string | `cofensetriage tag` |
**sort** | optional | Allows sorting the reports based on the 'updated_at' date of the report | string | |
**ingest_report** | optional | Allows ingestion of the report into the container | boolean | |
**ingest_subfields** | optional | Allows ingestion of the fields relating to the report into the container | boolean | |
**label** | optional | Allows ingestion of data into the container(s) with the provided label. The label must be valid or the action will fail. Required if 'ingest_report' or 'ingest_subfields' is set | string | |
**tenant** | optional | Allows creation of container(s) for the provided tenant ID or tenant name. The tenant must be valid or the action will fail. Required if 'ingest_report' or 'ingest_subfields' is set | string | |
**cef_mapping** | optional | JSON dictionary represented as a serialized JSON string. Each key in the dictionary is a potential key name in an artifact that is to be renamed to the value | string | |
**max_results** | optional | Maximum number of results to return | numeric | |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.parameter.location | string | `cofensetriage report location` | Processed |
action_result.parameter.from_address | string | `email` | test@example.com |
action_result.parameter.reporter_email | string | `email` | test@example.com |
action_result.parameter.subject | string | `cofensetriage report subject` | Demo |
action_result.parameter.match_priority | numeric | `cofensetriage priority` | 5 |
action_result.parameter.category_id | numeric | `cofensetriage category id` | 4 |
action_result.parameter.start_date | string | `date` | 2021-03-5 11:20:00 |
action_result.parameter.end_date | string | `date` | 2021-03-11 01:20:00 |
action_result.parameter.tags | string | `cofensetriage tag` | test |
action_result.parameter.categorization_tags | string | `cofensetriage tag` | test |
action_result.parameter.sort | string | | oldest_first latest_first |
action_result.parameter.ingest_report | boolean | | True False |
action_result.parameter.ingest_subfields | boolean | | False True |
action_result.parameter.label | string | | events |
action_result.parameter.tenant | string | | default |
action_result.parameter.cef_mapping | string | | |
action_result.parameter.max_results | numeric | | 5 |
action_result.data.\*.id | string | `cofensetriage report id` | 779 |
action_result.data.\*.meta.risk_score_summary.vip | numeric | | 5 |
action_result.data.\*.meta.risk_score_summary.rules | numeric | | 0 |
action_result.data.\*.meta.risk_score_summary.reporter | numeric | | 15 |
action_result.data.\*.meta.risk_score_summary.integrations | numeric | | 15 |
action_result.data.\*.type | string | | reports |
action_result.data.\*.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/779 |
action_result.data.\*.attributes.md5 | string | `md5` | bf858b01ec8e0fd8219ffff0c1606ff8 |
action_result.data.\*.attributes.sha256 | string | `sha256` | e520fe082f28de7bb25b9fa82de1e0b8ecea5922b06d5424b9829695c7c6fc06 |
action_result.data.\*.attributes.subject | string | `cofensetriage report subject` | Demo |
action_result.data.\*.attributes.location | string | `cofensetriage report location` | Processed |
action_result.data.\*.attributes.html_body | string | | |
action_result.data.\*.attributes.text_body | string | | |
action_result.data.\*.attributes.created_at | string | `date` | 2021-03-05T02:45:26.037Z |
action_result.data.\*.attributes.risk_score | numeric | | 35 |
action_result.data.\*.attributes.updated_at | string | `date` | 2021-03-11T12:19:35.470Z |
action_result.data.\*.attributes.raw_headers | string | | |
action_result.data.\*.attributes.received_at | string | `date` | 2021-03-05T02:38:59.000Z |
action_result.data.\*.attributes.reported_at | string | `date` | 2021-03-05T02:38:59.000Z |
action_result.data.\*.attributes.from_address | string | `email` | test@example.com |
action_result.data.\*.attributes.processed_at | string | `date` | 2021-03-11T12:19:33.337Z |
action_result.data.\*.attributes.match_priority | numeric | `cofensetriage priority` | 0 |
action_result.data.\*.attributes.categorization_tags | string | `cofensetriage tag` | test |
action_result.data.\*.attributes.tags | string | `cofensetriage tag` | test |
action_result.data.\*.container_id | numeric | `container id` | 240 |
action_result.data.\*.relationships.urls.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/779/relationships/urls |
action_result.data.\*.relationships.urls.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/779/urls |
action_result.data.\*.relationships.rules.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/779/relationships/rules |
action_result.data.\*.relationships.rules.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/779/rules |
action_result.data.\*.relationships.cluster.data.id | string | | 255 |
action_result.data.\*.relationships.cluster.data.type | string | | clusters |
action_result.data.\*.relationships.cluster.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/779/relationships/cluster |
action_result.data.\*.relationships.cluster.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/779/cluster |
action_result.data.\*.relationships.headers.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/779/relationships/headers |
action_result.data.\*.relationships.headers.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/779/headers |
action_result.data.\*.relationships.assignee.data.id | string | | 1 |
action_result.data.\*.relationships.assignee.data.type | string | | assignees |
action_result.data.\*.relationships.assignee.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/779/relationships/assignee |
action_result.data.\*.relationships.assignee.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/779/assignee |
action_result.data.\*.relationships.category.data.id | string | `cofensetriage category id` | 6 |
action_result.data.\*.relationships.category.data.type | string | | categories |
action_result.data.\*.relationships.category.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/779/relationships/category |
action_result.data.\*.relationships.category.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/779/category |
action_result.data.\*.relationships.reporter.data.id | string | `cofensetriage reporter id` | 24 |
action_result.data.\*.relationships.reporter.data.type | string | | reporters |
action_result.data.\*.relationships.reporter.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/779/relationships/reporter |
action_result.data.\*.relationships.reporter.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/779/reporter |
action_result.data.\*.relationships.hostnames.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/779/relationships/hostnames |
action_result.data.\*.relationships.hostnames.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/779/hostnames |
action_result.data.\*.relationships.attachments.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/779/relationships/attachments |
action_result.data.\*.relationships.attachments.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/779/attachments |
action_result.data.\*.relationships.threat_indicators.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/779/relationships/threat_indicators |
action_result.data.\*.relationships.threat_indicators.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/779/threat_indicators |
action_result.data.\*.relationships.attachment_payloads.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/779/relationships/attachment_payloads |
action_result.data.\*.relationships.attachment_payloads.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/779/attachment_payloads |
action_result.status | string | | success failed |
action_result.message | string | | Total reports retrieved: 15 |
action_result.summary | string | | |
action_result.summary.total_reports_retrieved | numeric | | 15 |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |
action_result.data.\*.attributes.urls_count | numeric | | 12 |
action_result.data.\*.attributes.rules_count | numeric | | 2 |
action_result.data.\*.attributes.comments_count | numeric | | 1 |
action_result.data.\*.attributes.attachments_count | numeric | | 0 |
action_result.data.\*.attributes.first_processed_at | string | | 2022-03-01T07:14:34.040Z |
action_result.data.\*.relationships.domains.links.self | string | | https://test.testcloud.com/api/public/v2/reports/1/relationships/domains |
action_result.data.\*.relationships.domains.links.related | string | | https://test.testcloud.com/api/public/v2/reports/1/domains |
action_result.data.\*.relationships.assignee.data | string | | |
action_result.data.\*.relationships.comments.links.self | string | | https://test.testcloud.com/api/public/v2/reports/1/relationships/comments |
action_result.data.\*.relationships.comments.links.related | string | | https://test.testcloud.com/api/public/v2/reports/1/comments |
action_result.data.\*.relationships.processed_by.data.id | string | | 1 |
action_result.data.\*.relationships.processed_by.data.type | string | | api_applications |
action_result.data.\*.relationships.processed_by.links.self | string | | https://test.testcloud.com/api/public/v2/reports/1/relationships/processed_by |
action_result.data.\*.relationships.processed_by.links.related | string | | https://test.testcloud.com/api/public/v2/reports/1/processed_by |
action_result.data.\*.relationships.cofense_intelligence_indicators.links.self | string | | https://test.testcloud.com/api/public/v2/reports/1/relationships/cofense_intelligence_indicators |
action_result.data.\*.relationships.cofense_intelligence_indicators.links.related | string | | https://test.testcloud.com/api/public/v2/reports/1/cofense_intelligence_indicators |
action_result.data.\*.relationships.processed_by.data | string | | |
action_result.data.\*.relationships.cluster.data | string | | |
action_result.data.\*.relationships.category.data | string | | |

## action: 'get report'

Retrieve a report with the provided ID from the Cofense Triage Platform

Type: **investigate** \
Read only: **True**

If the 'ingest_subfields' parameter is true, the report and the subfields together will get ingested into the container.

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**report_id** | required | The ID of the report which is to be fetched | numeric | `cofensetriage report id` |
**ingest_report** | optional | Allow ingestion of the report into the container | boolean | |
**ingest_subfields** | optional | Ingestion of the fields relating to the report into the container | boolean | |
**label** | optional | Allows ingestion of data into the container(s) with the provided label. The label must be valid or the action will fail. Required if 'ingest_report' or 'ingest_subfields' is set | string | |
**tenant** | optional | Allows creation of container(s) for the provided tenant ID or tenant name. The tenant must be valid or the action will fail. Required if 'ingest_report' or 'ingest_subfields' is set | string | |
**cef_mapping** | optional | JSON dictionary represented as a serialized JSON string. Each key in the dictionary is a potential key name in an artifact that is to be renamed to the value | string | |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.parameter.report_id | numeric | `cofensetriage report id` | 781 |
action_result.parameter.ingest_report | boolean | | False True |
action_result.parameter.ingest_subfields | boolean | | False True |
action_result.parameter.label | string | | events |
action_result.parameter.tenant | string | | default |
action_result.parameter.cef_mapping | string | | |
action_result.data.\*.id | string | `cofensetriage report id` | 781 |
action_result.data.\*.container_id | numeric | `container id` | 781 |
action_result.data.\*.meta.risk_score_summary.vip | numeric | | 5 |
action_result.data.\*.meta.risk_score_summary.rules | numeric | | 0 |
action_result.data.\*.meta.risk_score_summary.reporter | numeric | | 15 |
action_result.data.\*.meta.risk_score_summary.integrations | numeric | | 0 |
action_result.data.\*.type | string | | reports |
action_result.data.\*.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/781 |
action_result.data.\*.attributes.md5 | string | `md5` | aadc9a5a046e00df0dcb2ffb7ddfa7b3 |
action_result.data.\*.attributes.sha256 | string | `sha256` | 157fa62949e9edbadc2f9a2dd8e9b34671d0f4b804bc7d6ed8259dac0c26e7cb |
action_result.data.\*.attributes.subject | string | `cofensetriage report subject` | Test mail |
action_result.data.\*.attributes.location | string | `cofensetriage report location` | Reconnaissance |
action_result.data.\*.attributes.html_body | string | | |
action_result.data.\*.attributes.text_body | string | | |
action_result.data.\*.attributes.created_at | string | `date` | 2021-03-05T02:45:27.398Z |
action_result.data.\*.attributes.risk_score | numeric | | 20 |
action_result.data.\*.attributes.updated_at | string | `date` | 2021-03-05T02:45:28.899Z |
action_result.data.\*.attributes.raw_headers | string | | |
action_result.data.\*.attributes.received_at | string | `date` | 2021-03-05T02:37:48.000Z |
action_result.data.\*.attributes.reported_at | string | `date` | 2021-03-05T02:37:46.000Z |
action_result.data.\*.attributes.from_address | string | `email` | test@example.com |
action_result.data.\*.attributes.processed_at | string | `date` | 2021-03-05T02:40:46.000Z |
action_result.data.\*.attributes.match_priority | numeric | `cofensetriage priority` | 0 |
action_result.data.\*.attributes.categorization_tags | string | `cofensetriage tag` | test |
action_result.data.\*.attributes.tags | string | `cofensetriage tag` | test |
action_result.data.\*.relationships.urls.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/781/relationships/urls |
action_result.data.\*.relationships.urls.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/781/urls |
action_result.data.\*.relationships.rules.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/781/relationships/rules |
action_result.data.\*.relationships.rules.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/781/rules |
action_result.data.\*.relationships.cluster.data.id | string | | 255 |
action_result.data.\*.relationships.cluster.data.type | string | | clusters |
action_result.data.\*.relationships.cluster.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/781/relationships/cluster |
action_result.data.\*.relationships.cluster.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/781/cluster |
action_result.data.\*.relationships.headers.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/781/relationships/headers |
action_result.data.\*.relationships.headers.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/781/headers |
action_result.data.\*.relationships.assignee.data.id | string | | 1 |
action_result.data.\*.relationships.assignee.data.type | string | | assignees |
action_result.data.\*.relationships.assignee.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/781/relationships/assignee |
action_result.data.\*.relationships.assignee.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/781/assignee |
action_result.data.\*.relationships.category.data.id | string | `cofensetriage category id` | 6 |
action_result.data.\*.relationships.category.data.type | string | | categories |
action_result.data.\*.relationships.category.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/781/relationships/category |
action_result.data.\*.relationships.category.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/781/category |
action_result.data.\*.relationships.reporter.data.id | string | `cofensetriage reporter id` | 24 |
action_result.data.\*.relationships.reporter.data.type | string | | reporters |
action_result.data.\*.relationships.reporter.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/781/relationships/reporter |
action_result.data.\*.relationships.reporter.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/781/reporter |
action_result.data.\*.relationships.hostnames.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/781/relationships/hostnames |
action_result.data.\*.relationships.hostnames.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/781/hostnames |
action_result.data.\*.relationships.attachments.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/781/relationships/attachments |
action_result.data.\*.relationships.attachments.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/781/attachments |
action_result.data.\*.relationships.threat_indicators.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/781/relationships/threat_indicators |
action_result.data.\*.relationships.threat_indicators.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/781/threat_indicators |
action_result.data.\*.relationships.attachment_payloads.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/781/relationships/attachment_payloads |
action_result.data.\*.relationships.attachment_payloads.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/781/attachment_payloads |
action_result.status | string | | success failed |
action_result.message | string | | Successfully fetched the report |
action_result.summary | string | | |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'get email'

Downloads the raw email for the report that matches the specified report ID

Type: **investigate** \
Read only: **True**

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**report_id** | required | The ID of the report | numeric | `cofensetriage report id` |
**download_method** | required | Allows the user to download the email as an artifact or as a vaulted file | string | |
**create_vaulted_file_artifact** | optional | If storing as a vaulted file, this parameter allows the user to create an artifact referencing that file | boolean | |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.parameter.create_vaulted_file_artifact | boolean | | True False |
action_result.parameter.download_method | string | | artifact vaulted file |
action_result.parameter.report_id | numeric | `cofensetriage report id` | 1 |
action_result.data.\*.artifact_id | string | `artifact id` | 2 |
action_result.data.\*.filename | string | `file name` | test.eml |
action_result.data.\*.md5 | string | `md5` `hash` | 17c200f0a14e1cbe23c04343c5d858ee |
action_result.data.\*.report_id | string | `cofensetriage report id` | 1 |
action_result.data.\*.sha1 | string | `sha1` `hash` | 4ef03a5e510cb4a930c51ceaa6110928a8f99257 |
action_result.data.\*.sha256 | string | `sha256` `hash` | a949bb915fa346d56522455ba2d598653b1a42197437395f30b906079e67d8bb |
action_result.data.\*.size | string | | 31960 |
action_result.data.\*.vault_id | string | `vault id` | 4ef03a5e510cb4a930c51ceaa6110928a8f99257 |
action_result.data.\*.vaulted | string | `file path` | /vault/path/4ef03a5e510cb4a930c51ceaa6110928a8f99257 |
action_result.status | string | | success failed |
action_result.message | string | | Vault id: 998c8298597498169d7eaae7d8a9d2146475a156, Filename: report_10.eml, Artifact id: 11321, Report id: 10 |
action_result.summary.filename | string | `file name` | report_1.eml |
action_result.summary.vault_id | string | `vault id` | 998c8298597498169d7eaae7d8a9d2146475a156 |
action_result.summary.report_id | numeric | `cofensetriage report id` | 1 |
action_result.summary.artifact_id | numeric | `artifact id` | 1094 |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'get categories'

Retrieve categories from the Cofense Triage Platform filtered based on the provided parameters

Type: **investigate** \
Read only: **True**

If no value is provided in any parameter, then all the records will be retrieved.

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**name** | optional | Allows the user to fetch the categories with the name containing a specific string | string | `cofensetriage category name` |
**malicious** | optional | Allows the user to fetch the categories based on whether the category is used to classify malicious reports or not | boolean | |
**max_results** | optional | Maximum number of results to return | numeric | |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.parameter.name | string | `cofensetriage category name` | Non-Malicious |
action_result.parameter.malicious | boolean | | False True |
action_result.parameter.max_results | numeric | | 100 |
action_result.data.\*.id | string | `cofensetriage category id` | 1 |
action_result.data.\*.type | string | | categories |
action_result.data.\*.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/categories/1 |
action_result.data.\*.attributes.name | string | `cofensetriage category name` | Non-Malicious |
action_result.data.\*.attributes.color | string | | #739d75 |
action_result.data.\*.attributes.score | numeric | | -5 |
action_result.data.\*.attributes.archived | boolean | | False True |
action_result.data.\*.attributes.malicious | boolean | | False True |
action_result.data.\*.attributes.created_at | string | `date` | 2020-10-21T15:30:56.280Z |
action_result.data.\*.attributes.updated_at | string | `date` | 2020-10-21T15:30:56.280Z |
action_result.data.\*.relationships.reports.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/categories/1/relationships/reports |
action_result.data.\*.relationships.reports.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/categories/1/reports |
action_result.data.\*.relationships.one_clicks.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/categories/1/relationships/one_clicks |
action_result.data.\*.relationships.one_clicks.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/categories/1/one_clicks |
action_result.status | string | | success failed |
action_result.message | string | | Total categories retrieved: 1 |
action_result.summary.total_categories_retrieved | numeric | | 10 |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'get responses'

Retrieve responses from the Cofense Triage Platform. This action is supported for Cofense Triage with version older than 1.23

Type: **investigate** \
Read only: **True**

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**max_results** | optional | Allows the user to limit the number of results | numeric | |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.parameter.max_results | numeric | | 100 |
action_result.data.\*.id | string | `cofensetirage response id` | 10 |
action_result.data.\*.relationships.one_clicks.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/responses/1/relationships/one_clicks |
action_result.data.\*.relationships.one_clicks.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/responses/1/one_clicks |
action_result.data.\*.attributes.body | string | | Body of the email |
action_result.data.\*.attributes.name | string | | Display name of the email |
action_result.data.\*.attributes.to_other | boolean | | False True |
action_result.data.\*.attributes.created_at | string | `date` | 2021-03-05T02:45:27.398Z |
action_result.data.\*.attributes.updated_at | string | `date` | 2021-03-05T02:45:27.398Z |
action_result.data.\*.attributes.bcc_address | string | `email` | test@example.com |
action_result.data.\*.attributes.cc_address | string | `email` | test@example.com |
action_result.data.\*.attributes.attach_original | boolean | | False True |
action_result.data.\*.attributes.to_other_address | string | `email` | test@example.com |
action_result.data.\*.attributes.subject | string | | Subject of the email |
action_result.data.\*.attributes.to_reporter | boolean | | False True |
action_result.data.\*.attributes.description | string | | Description of the email |
action_result.data.\*.type | string | | responses |
action_result.data.\*.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/responses/1 |
action_result.status | string | | success failed |
action_result.message | string | | Total responses retrieved: 10 |
action_result.summary.total_responses_retrieved | numeric | | 1 |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'create response'

Create a response. This action is supported for Cofense Triage with version older than 1.23

Type: **generic** \
Read only: **False**

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**name** | required | Display name of the response sent to individuals | string | |
**subject** | required | Subject of the response | string | |
**body** | required | Body of the email | string | |
**description** | optional | Description of the response | string | |
**to_reporter** | optional | To add the reporter to the response recipient list or not | boolean | |
**to_other** | optional | To add the addresses specified in 'to_other_address' to the response recipient list or not | boolean | |
**to_other_address** | optional | Comma-separated list of email addresses to send the response to | string | `email` |
**attach_original** | optional | To attach the original email to the response or not | boolean | |
**cc_address** | optional | Comma-separated list of email addresses to CC the response to | string | `email` |
**bcc_address** | optional | Comma-separated list of email addresses to BCC the response to | string | `email` |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.parameter.name | string | | Display name of the response |
action_result.parameter.subject | string | | Subject of the response |
action_result.parameter.body | string | | Body of the response |
action_result.parameter.description | string | | Description of the response |
action_result.parameter.to_reporter | boolean | | False True |
action_result.parameter.to_other | boolean | | False True |
action_result.parameter.to_other_address | string | `email` | test@example.com |
action_result.parameter.attach_original | boolean | | False True |
action_result.parameter.cc_address | string | `email` | test@example.com |
action_result.parameter.bcc_address | string | `email` | test@example.com |
action_result.data.\*.id | string | `cofensetirage response id` | 10 |
action_result.data.\*.relationships.one_clicks.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/responses/1/relationships/one_clicks |
action_result.data.\*.relationships.one_clicks.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/responses/46/one_clicks |
action_result.data.\*.attributes.body | string | | Body of the response |
action_result.data.\*.attributes.name | string | | Display name of the response |
action_result.data.\*.attributes.to_other | boolean | | False True |
action_result.data.\*.attributes.created_at | string | `date` | 2021-03-05T02:45:27.398Z |
action_result.data.\*.attributes.updated_at | string | `date` | 2021-03-05T02:45:27.398Z |
action_result.data.\*.attributes.bcc_address | string | `email` | test@example.com |
action_result.data.\*.attributes.cc_address | string | `email` | test@example.com |
action_result.data.\*.attributes.attach_original | boolean | | False True |
action_result.data.\*.attributes.to_other_address | string | `email` | test@example.com |
action_result.data.\*.attributes.subject | string | | Subject of the response |
action_result.data.\*.attributes.to_reporter | boolean | | False True |
action_result.data.\*.attributes.description | string | | Description of the response |
action_result.data.\*.type | string | | responses |
action_result.data.\*.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/responses/1 |
action_result.status | string | | success failed |
action_result.message | string | | Successfully created the response. |
action_result.summary.response_id | string | `cofensetirage response id` | 10 |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'categorize report'

Categorize a report into the provided category

Type: **generic** \
Read only: **False**

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**report_id** | required | The ID of the report | numeric | `cofensetriage report id` |
**category_id** | optional | The ID of the category | numeric | `cofensetriage category id` |
**category_name** | optional | The name of the category | string | `cofensetriage category name` |
**response_id** | optional | The ID of the response | numeric | |
**categorization_tags** | optional | Allows the user to provide multiple tags to the report while categorizing it | string | `cofensetriage tag` |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.parameter.report_id | numeric | `cofensetriage report id` | 796 |
action_result.parameter.response_id | numeric | | 3 10 |
action_result.parameter.category_name | string | `cofensetriage category name` | API-Cluster spam |
action_result.parameter.category_id | numeric | `cofensetriage category id` | 2 |
action_result.parameter.categorization_tags | string | `cofensetriage tag` | test1, test2 |
action_result.data | string | | |
action_result.status | string | | success failed |
action_result.message | string | | Successfully categorized the report |
action_result.summary | string | | |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'get threat indicators'

Retrieve threat indicators from the Cofense Triage Platform filtered based on the provided parameters

Type: **investigate** \
Read only: **True**

If the 'ingest_subfields' parameter is true, the threat indicator and the subfields together will get ingested into the container. If no value is provided in any parameter, then all the records will be retrieved.

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**level** | optional | The level of the threat indicator | string | `cofensetriage threat indicator level` |
**type** | optional | Type of the threat indicators | string | `cofensetriage threat indicator type` |
**source** | optional | Source of the threat indicators | string | `cofensetriage threat indicator source` |
**value** | optional | Value of the threat indicators | string | `sha256` `md5` `url` `hash` `domain` `host name` |
**start_date** | optional | Threat indicators updated on or after the provided date | string | `date` |
**end_date** | optional | Threat indicators updated before the provided date | string | `date` |
**sort** | optional | Sorting based on updated date of threat indicators | string | |
**ingest_threat_indicator** | optional | Ingestion of threat indicator(s) into the container(s) | boolean | |
**ingest_subfields** | optional | Allow ingestion of the fields relating to the threat indicator into the container | boolean | |
**label** | optional | Allows ingestion of data into the container(s) with the provided label. The label must be valid or the action will fail. Required if 'ingest_threat_indicator' or 'ingest_subfields' is set | string | |
**tenant** | optional | Allows creation of container(s) for the provided tenant ID or tenant name. The tenant must be valid or the action will fail. Required if 'ingest_threat_indicator' or 'ingest_subfields' is set | string | |
**cef_mapping** | optional | JSON dictionary represented as a serialized JSON string | string | |
**max_results** | optional | Maximum number of results to return | numeric | |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.parameter.level | string | `cofensetriage threat indicator level` | Suspicious |
action_result.parameter.type | string | `cofensetriage threat indicator type` | url |
action_result.parameter.source | string | `cofensetriage threat indicator source` | Splunk_Phantom-UI |
action_result.parameter.value | string | `sha256` `md5` `url` `hash` `domain` `host name` | https://exampleurl.com |
action_result.parameter.start_date | string | `date` | 2020-11-18T02:29:07.633Z |
action_result.parameter.end_date | string | `date` | 2020-11-18T02:29:07.633Z |
action_result.parameter.sort | string | | latest_first |
action_result.parameter.ingest_threat_indicator | boolean | | False True |
action_result.parameter.ingest_subfields | boolean | | False True |
action_result.parameter.label | string | | events |
action_result.parameter.tenant | string | | 0 |
action_result.parameter.cef_mapping | string | | |
action_result.parameter.max_results | numeric | | 100 |
action_result.data.\*.id | string | `cofensetriage threat indicator id` | 24 |
action_result.data.\*.type | string | | threat_indicators |
action_result.data.\*.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/threat_indicators/24 |
action_result.data.\*.attributes.created_at | string | `date` | 2020-11-03T19:35:20.636Z |
action_result.data.\*.attributes.updated_at | string | `date` | 2020-11-03T19:35:20.643Z |
action_result.data.\*.attributes.threat_type | string | `cofensetriage threat indicator type` | URL |
action_result.data.\*.attributes.threat_level | string | `cofensetriage threat indicator level` | Suspicious |
action_result.data.\*.attributes.threat_value | string | `sha256` `md5` `url` `hash` `domain` `host name` | https://exampleurl.com |
action_result.data.\*.attributes.threat_source | string | `cofensetriage threat indicator source` | Triage-UI |
action_result.data.\*.relationships.owner.data.id | string | | 2 |
action_result.data.\*.relationships.owner.data.type | string | | operators |
action_result.data.\*.relationships.owner.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/threat_indicators/24/relationships/owner |
action_result.data.\*.relationships.owner.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/threat_indicators/24/owner |
action_result.data.\*.relationships.reports.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/threat_indicators/24/relationships/reports |
action_result.data.\*.relationships.reports.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/threat_indicators/24/reports |
action_result.data.\*.relationships.comments.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/threat_indicators/24/relationships/comments |
action_result.data.\*.relationships.comments.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/threat_indicators/24/comments |
action_result.data.\*.container_id | numeric | `container id` | 347 |
action_result.status | string | | success failed |
action_result.message | string | | Total threat indicators retrieved: 1 |
action_result.summary.total_threat_indicators_retrieved | numeric | | 1 |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'create threat indicator'

Create a threat indicator with the provided parameters

Type: **generic** \
Read only: **False**

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**level** | required | The level of the threat indicator | string | `cofensetriage threat indicator level` |
**type** | required | Type of the threat indicator | string | `cofensetriage threat indicator type` |
**value** | required | Value of the threat indicator | string | `sha256` `md5` `url` `hostname` `domain` `hash` |
**source** | optional | Source of the threat indicator | string | `cofensetriage threat indicator source` |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.parameter.level | string | `cofensetriage threat indicator level` | Suspicious |
action_result.parameter.type | string | `cofensetriage threat indicator type` | URL |
action_result.parameter.value | string | `sha256` `md5` `url` `hostname` `domain` `hash` | https://exampleurl.com |
action_result.parameter.source | string | `cofensetriage threat indicator source` | Splunk_Phantom-UI |
action_result.data.\*.id | string | `cofensetriage threat indicator id` | 209 |
action_result.data.\*.type | string | | threat_indicators |
action_result.data.\*.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/threat_indicators/209 |
action_result.data.\*.attributes.created_at | string | `date` | 2021-03-31T05:13:14.368Z |
action_result.data.\*.attributes.updated_at | string | `date` | 2021-03-31T05:13:14.368Z |
action_result.data.\*.attributes.threat_type | string | `cofensetriage threat indicator type` | URL |
action_result.data.\*.attributes.threat_level | string | `cofensetriage threat indicator level` | Suspicious |
action_result.data.\*.attributes.threat_value | string | `sha256` `md5` `url` `hostname` `hash` `domain` | https://exampleurl.com |
action_result.data.\*.attributes.threat_source | string | `cofensetriage threat indicator source` | Splunk_Phantom-UI |
action_result.data.\*.relationships.owner.data.id | string | | 3 |
action_result.data.\*.relationships.owner.data.type | string | | oauth_applications |
action_result.data.\*.relationships.owner.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/threat_indicators/209/relationships/owner |
action_result.data.\*.relationships.owner.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/threat_indicators/209/owner |
action_result.data.\*.relationships.reports.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/threat_indicators/209/relationships/reports |
action_result.data.\*.relationships.reports.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/threat_indicators/209/reports |
action_result.data.\*.relationships.comments.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/threat_indicators/209/relationships/comments |
action_result.data.\*.relationships.comments.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/threat_indicators/209/comments |
action_result.status | string | | success failed |
action_result.message | string | | Successfully created the threat indicator |
action_result.summary.threat_indicator_id | string | | 15 |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'get reporters'

Retrieve reporters from the Cofense Triage Platform filtered based on the provided parameters

Type: **investigate** \
Read only: **True**

If no value is provided in any parameter, then all the records will be retrieved.

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**vip** | optional | Allows searching for the VIP reporters | boolean | |
**reputation_score** | optional | Allows searching for reporters having the provided reputation score. It allows a comma-separated list | string | `cofensetriage reporter reputation score` |
**email** | optional | Allows searching for the reporter with a specific email | string | `email` |
**sort** | optional | Allows sorting the reporters based on the ID | string | |
**max_results** | optional | Maximum number of results to return | numeric | |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.parameter.vip | boolean | | False True |
action_result.parameter.reputation_score | string | `cofensetriage reporter reputation score` | 5 |
action_result.parameter.email | string | `email` | test@example.com |
action_result.parameter.sort | string | | oldest_first |
action_result.parameter.max_results | numeric | | 100 |
action_result.data.\*.id | string | `cofensetriage reporter id` | 4 |
action_result.data.\*.type | string | | reporters |
action_result.data.\*.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reporters/4 |
action_result.data.\*.attributes.vip | boolean | | False True |
action_result.data.\*.attributes.email | string | `email` | test@example.com |
action_result.data.\*.attributes.created_at | string | `date` | 2020-10-21T20:54:23.383Z |
action_result.data.\*.attributes.updated_at | string | `date` | 2020-12-11T13:33:53.457Z |
action_result.data.\*.attributes.reports_count | numeric | | 10 |
action_result.data.\*.attributes.last_reported_at | string | `date` | 2020-12-11T05:46:39.000Z |
action_result.data.\*.attributes.reputation_score | numeric | `cofensetriage reporter reputation score` | 13 |
action_result.data.\*.relationships.reports.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reporters/4/relationships/reports |
action_result.data.\*.relationships.reports.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/reporters/4/reports |
action_result.data.\*.relationships.clusters.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reporters/4/relationships/clusters |
action_result.data.\*.relationships.clusters.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/reporters/4/clusters |
action_result.status | string | | success failed |
action_result.message | string | | Total reporters retrieved: 2 |
action_result.summary.total_reporters_retrieved | numeric | | 96 |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'get reporter'

Retrieve a reporter from the Cofense Triage Platform for the provided reporter ID

Type: **investigate** \
Read only: **True**

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**reporter_id** | required | The unique ID of the reporter | numeric | `cofensetriage reporter id` |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.parameter.reporter_id | numeric | `cofensetriage reporter id` | 4 |
action_result.data.\*.id | string | `cofensetriage reporter id` | 4 |
action_result.data.\*.type | string | | reporters |
action_result.data.\*.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reporters/4 |
action_result.data.\*.attributes.vip | boolean | | False True |
action_result.data.\*.attributes.email | string | `email` | test@example.com |
action_result.data.\*.attributes.created_at | string | `date` | 2020-10-21T20:54:23.383Z |
action_result.data.\*.attributes.updated_at | string | `date` | 2020-12-11T13:33:53.457Z |
action_result.data.\*.attributes.reports_count | numeric | | 10 |
action_result.data.\*.attributes.last_reported_at | string | `date` | 2020-12-11T05:46:39.000Z |
action_result.data.\*.attributes.reputation_score | numeric | `cofensetriage reporter reputation score` | 13 |
action_result.data.\*.relationships.reports.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reporters/4/relationships/reports |
action_result.data.\*.relationships.reports.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/reporters/4/reports |
action_result.data.\*.relationships.clusters.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reporters/4/relationships/clusters |
action_result.data.\*.relationships.clusters.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/reporters/4/clusters |
action_result.status | string | | success failed |
action_result.message | string | | Successfully retrieved the reporter |
action_result.summary | string | | |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'get urls'

Retrieve URLs from the Cofense Triage Platform filtered based on the provided parameters

Type: **investigate** \
Read only: **True**

If no value is provided in any parameter, then all the records will be retrieved.

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**risk_score** | optional | Risk score of the URL | numeric | `cofensetriage risk score` |
**risk_score_operator** | optional | Operator to work with the risk score parameter | string | |
**url_value** | optional | Value of the URL to search for | string | `url` |
**start_date** | optional | Allows filtering the URLs updated on or after the provided date | string | `date` |
**end_date** | optional | Allows filtering the URLs updated before the provided date | string | `date` |
**sort** | optional | Allows sorting the URLs based on the 'updated_at' date | string | |
**max_results** | optional | Maximum number of results to return | numeric | |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.parameter.risk_score | numeric | `cofensetriage risk score` | 2 |
action_result.parameter.risk_score_operator | string | | eq |
action_result.parameter.url_value | string | `url` | http://testurl.com |
action_result.parameter.start_date | string | `date` | 2021-03-5 11:20:00 |
action_result.parameter.end_date | string | `date` | 2021-03-11 01:20:00 |
action_result.parameter.sort | string | | oldest_first |
action_result.parameter.max_results | numeric | | 100 |
action_result.data.\*.id | string | `cofensetriage url id` | 15 |
action_result.data.\*.type | string | | urls |
action_result.data.\*.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/urls/15 |
action_result.data.\*.attributes.url | string | `url` | http://testurl.com |
action_result.data.\*.attributes.created_at | string | `date` | 2020-10-21T20:54:24.185Z |
action_result.data.\*.attributes.risk_score | string | `cofensetriage risk score` | |
action_result.data.\*.attributes.updated_at | string | `date` | 2020-10-21T20:54:24.185Z |
action_result.data.\*.relationships.reports.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/urls/15/relationships/reports |
action_result.data.\*.relationships.reports.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/urls/15/reports |
action_result.data.\*.relationships.clusters.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/urls/15/relationships/clusters |
action_result.data.\*.relationships.clusters.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/urls/15/clusters |
action_result.data.\*.relationships.hostname.data.id | string | | 6 |
action_result.data.\*.relationships.hostname.data.type | string | | hostnames |
action_result.data.\*.relationships.hostname.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/urls/15/relationships/hostname |
action_result.data.\*.relationships.hostname.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/urls/15/hostname |
action_result.status | string | | success failed |
action_result.message | string | | Total URLs retrieved: 2 |
action_result.summary.total_urls_retrieved | numeric | | 100 |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'get url'

Retrieve a URL from the Cofense Triage Platform for the provided URL ID

Type: **investigate** \
Read only: **True**

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**url_id** | required | ID of the URL | numeric | `cofensetriage url id` |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.parameter.url_id | numeric | `cofensetriage url id` | 15 |
action_result.data.\*.id | string | `cofensetriage url id` | 15 |
action_result.data.\*.type | string | | urls |
action_result.data.\*.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/urls/15 |
action_result.data.\*.attributes.url | string | `url` | http://testurl.com |
action_result.data.\*.attributes.created_at | string | `date` | 2020-10-21T20:54:24.185Z |
action_result.data.\*.attributes.risk_score | string | `cofensetriage risk score` | |
action_result.data.\*.attributes.updated_at | string | `date` | 2020-10-21T20:54:24.185Z |
action_result.data.\*.relationships.reports.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/urls/15/relationships/reports |
action_result.data.\*.relationships.reports.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/urls/15/reports |
action_result.data.\*.relationships.clusters.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/urls/15/relationships/clusters |
action_result.data.\*.relationships.clusters.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/urls/15/clusters |
action_result.data.\*.relationships.hostname.data.id | string | | 6 |
action_result.data.\*.relationships.hostname.data.type | string | | hostnames |
action_result.data.\*.relationships.hostname.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/urls/15/relationships/hostname |
action_result.data.\*.relationships.hostname.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/urls/15/hostname |
action_result.status | string | | success failed |
action_result.message | string | | Successfully retrieved the URL |
action_result.summary | string | | |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'get comments'

Retrieve comments from the Cofense Triage Platform filtered based on the provided parameters

Type: **investigate** \
Read only: **True**

If no value is provided in any parameter, then all the records will be retrieved.

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**body_format** | optional | Allows filtering the comments based on the format of the comment body | string | `cofensetriage comment body format` |
**tags** | optional | Allows filtering the comments based on the list of comma-separated tags. If the tag value contains a comma, enclose it in double-quotes (Example: tag1,"test,tag",tag2) | string | `cofensetriage tag` |
**start_date** | optional | Allows filtering the comments updated on or after the provided date | string | `date` |
**end_date** | optional | Allows filtering the comments updated before the provided date | string | `date` |
**sort** | optional | Allows sorting the comments based on the 'updated_at' date of the comment | string | |
**max_results** | optional | Maximum number of results to return | numeric | |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.parameter.body_format | string | `cofensetriage comment body format` | text |
action_result.parameter.tags | string | `cofensetriage tag` | test |
action_result.parameter.start_date | string | `date` | 2021-03-5 11:20:00 |
action_result.parameter.end_date | string | `date` | 2021-03-11 01:20:00 |
action_result.parameter.sort | string | | oldest_first latest_first |
action_result.parameter.max_results | numeric | | 5 |
action_result.data.\*.id | string | `cofensetriage comment id` | 15 |
action_result.data.\*.type | string | | comments |
action_result.data.\*.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/comments/1 |
action_result.data.\*.attributes.body | string | | |
action_result.data.\*.attributes.created_at | string | `date` | 2021-04-01T20:52:59.342Z |
action_result.data.\*.attributes.updated_at | string | `date` | 2021-04-01T20:52:59.342Z |
action_result.data.\*.attributes.body_format | string | `cofensetriage comment body format` | text |
action_result.data.\*.relationships.owner.data.id | string | | 2 |
action_result.data.\*.relationships.owner.data.type | string | | operators |
action_result.data.\*.relationships.owner.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/comments/1/relationships/owner |
action_result.data.\*.relationships.owner.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/comments/1/owner |
action_result.data.\*.relationships.commentable.data.id | string | | 216 |
action_result.data.\*.relationships.commentable.data.type | string | | threat indicator |
action_result.data.\*.relationships.commentable.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/comments/1/relationships/commentable |
action_result.data.\*.relationships.commentable.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/comments/1/commentable |
action_result.data.\*.attributes.body.type | string | | object |
action_result.data.\*.attributes.body.properties.from.type | string | `email` | test@example.net |
action_result.data.\*.attributes.body.properties.notes.type | string | | |
action_result.data.\*.attributes.body.properties.brands.type | string | | array |
action_result.data.\*.attributes.body.properties.brands.items.type | string | | string |
action_result.data.\*.attributes.body.properties.srctag.type | string | | Test |
action_result.data.\*.attributes.body.properties.sent_to.type | string | `email` | test@example.com |
action_result.data.\*.attributes.body.properties.subject.type | string | | |
action_result.data.\*.attributes.body.properties.summary.type | string | | |
action_result.data.\*.attributes.body.properties.reply_to.type | string | | |
action_result.data.\*.attributes.body.properties.report_id.type | string | | 804 |
action_result.data.\*.attributes.body.properties.message_id.type | string | | |
action_result.data.\*.attributes.body.properties.phenotypes.type | string | | |
action_result.data.\*.attributes.body.properties.report_url.type | string | `url` | https://cofensetriageurl.com/reports/804 |
action_result.data.\*.attributes.body.properties.reported_by.type | string | `email` | test@example.com |
action_result.data.\*.attributes.body.properties.stage_1_iocs.type | string | | object |
action_result.data.\*.attributes.body.properties.stage_1_iocs.properties.files.type | string | | subscription.xlsb |
action_result.data.\*.attributes.body.properties.stage_1_iocs.properties.infection_ips.type | string | | array |
action_result.data.\*.attributes.body.properties.stage_1_iocs.properties.infection_ips.items.type | string | | string |
action_result.data.\*.attributes.body.properties.stage_1_iocs.properties.infection_urls.type | string | | array |
action_result.data.\*.attributes.body.properties.stage_1_iocs.properties.infection_urls.items.type | string | | https://example.org |
action_result.data.\*.attributes.body.properties.stage_2_iocs.type | string | | object |
action_result.data.\*.attributes.body.properties.stage_2_iocs.properties.md5.type | string | | af18cd9e099e6e7c56bd5a07502b1f0z |
action_result.data.\*.attributes.body.properties.stage_2_iocs.properties.size.type | string | | 37,888 |
action_result.data.\*.attributes.body.properties.stage_2_iocs.properties.files.type | string | `file name` | 172.dll |
action_result.data.\*.attributes.body.properties.stage_2_iocs.properties.c2_ips.type | string | `ip` | 33.162.31.92 |
action_result.data.\*.attributes.body.properties.stage_2_iocs.properties.c2_urls.type | string | | http://example.net |
action_result.data.\*.attributes.body.properties.stage_2_iocs.properties.payload_ips.type | string | | array |
action_result.data.\*.attributes.body.properties.stage_2_iocs.properties.payload_ips.items.type | string | `ip` | 55.220.162.4 |
action_result.data.\*.attributes.body.properties.stage_2_iocs.properties.payload_urls.type | string | | array |
action_result.data.\*.attributes.body.properties.stage_2_iocs.properties.payload_urls.items.type | string | | http://example.com |
action_result.data.\*.attributes.body.properties.received_time.type | string | | Mar 31, 2021 at 14:40:13 UTC |
action_result.data.\*.attributes.body.properties.reported_time.type | string | | Mar 31, 2021 at 14:40:45 UTC |
action_result.data.\*.attributes.body.properties.vision_results.type | string | | object |
action_result.data.\*.attributes.body.properties.vision_results.properties.results_id | string | | 61 |
action_result.data.\*.attributes.body.properties.vision_results.properties.query_created.type | string | | Apr 2, 2021 at 14:37:35 UTC |
action_result.data.\*.attributes.body.properties.vision_results.properties.messages_found | string | | 2 |
action_result.data.\*.attributes.body.properties.vision_results.properties.messages_removed | string | | 0 |
action_result.data.\*.attributes.body.properties.escalation_type.type | string | | |
action_result.data.\*.attributes.body.properties.malware_families.type | string | | |
action_result.data.\*.attributes.tags | string | `cofensetriage tag` | TEST |
action_result.status | string | | success failed |
action_result.message | string | | Total comments retrieved: 16 |
action_result.summary.total_comments_retrieved | numeric | | 16 |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'get comment'

Retrieve a comment from the Cofense Triage Platform for the provided comment ID

Type: **investigate** \
Read only: **True**

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**comment_id** | required | ID of the comment | numeric | `cofensetriage comment id` |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.parameter.comment_id | numeric | `cofensetriage comment id` | 15 |
action_result.data.\*.id | string | `cofensetriage comment id` | 15 |
action_result.data.\*.type | string | | comments |
action_result.data.\*.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/comments/1 |
action_result.data.\*.attributes.body | string | | Test comment |
action_result.data.\*.attributes.created_at | string | `date` | 2021-04-01T20:52:59.342Z |
action_result.data.\*.attributes.updated_at | string | `date` | 2021-04-01T20:52:59.342Z |
action_result.data.\*.attributes.body_format | string | `cofensetriage comment body format` | text |
action_result.data.\*.relationships.owner.data.id | string | | 2 |
action_result.data.\*.relationships.owner.data.type | string | | operators |
action_result.data.\*.relationships.owner.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/comments/1/relationships/owner |
action_result.data.\*.relationships.owner.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/comments/1/owner |
action_result.data.\*.relationships.commentable.data.id | string | | 216 |
action_result.data.\*.relationships.commentable.data.type | string | | threat indicator |
action_result.data.\*.relationships.commentable.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/comments/1/relationships/commentable |
action_result.data.\*.relationships.commentable.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/comments/1/commentable |
action_result.data.\*.attributes.body.type | string | | object |
action_result.data.\*.attributes.body.properties.from.type | string | `email` | test@example.net |
action_result.data.\*.attributes.body.properties.notes.type | string | | |
action_result.data.\*.attributes.body.properties.brands.type | string | | array |
action_result.data.\*.attributes.body.properties.brands.items.type | string | | string |
action_result.data.\*.attributes.body.properties.srctag.type | string | | Test |
action_result.data.\*.attributes.body.properties.sent_to.type | string | `email` | test@example.com |
action_result.data.\*.attributes.body.properties.subject.type | string | | |
action_result.data.\*.attributes.body.properties.summary.type | string | | |
action_result.data.\*.attributes.body.properties.reply_to.type | string | | |
action_result.data.\*.attributes.body.properties.report_id.type | string | | 804 |
action_result.data.\*.attributes.body.properties.message_id.type | string | | |
action_result.data.\*.attributes.body.properties.phenotypes.type | string | | |
action_result.data.\*.attributes.body.properties.report_url.type | string | `url` | https://cofensetriageurl.com/reports/804 |
action_result.data.\*.attributes.body.properties.reported_by.type | string | `email` | test@example.com |
action_result.data.\*.attributes.body.properties.stage_1_iocs.type | string | | object |
action_result.data.\*.attributes.body.properties.stage_1_iocs.properties.files.type | string | | subscription.xlsb |
action_result.data.\*.attributes.body.properties.stage_1_iocs.properties.infection_ips.type | string | | array |
action_result.data.\*.attributes.body.properties.stage_1_iocs.properties.infection_ips.items.type | string | | string |
action_result.data.\*.attributes.body.properties.stage_1_iocs.properties.infection_urls.type | string | | array |
action_result.data.\*.attributes.body.properties.stage_1_iocs.properties.infection_urls.items.type | string | | https://example.org |
action_result.data.\*.attributes.body.properties.stage_2_iocs.type | string | | object |
action_result.data.\*.attributes.body.properties.stage_2_iocs.properties.md5.type | string | | af18cd9e099e6e7c56bd5a07502b1f0z |
action_result.data.\*.attributes.body.properties.stage_2_iocs.properties.size.type | string | | 37,888 |
action_result.data.\*.attributes.body.properties.stage_2_iocs.properties.files.type | string | `file name` | 172.dll |
action_result.data.\*.attributes.body.properties.stage_2_iocs.properties.c2_ips.type | string | `ip` | 33.162.31.92 |
action_result.data.\*.attributes.body.properties.stage_2_iocs.properties.c2_urls.type | string | | http://example.net |
action_result.data.\*.attributes.body.properties.stage_2_iocs.properties.payload_ips.type | string | | array |
action_result.data.\*.attributes.body.properties.stage_2_iocs.properties.payload_ips.items.type | string | `ip` | 55.220.162.4 |
action_result.data.\*.attributes.body.properties.stage_2_iocs.properties.payload_urls.type | string | | array |
action_result.data.\*.attributes.body.properties.stage_2_iocs.properties.payload_urls.items.type | string | | http://example.com |
action_result.data.\*.attributes.body.properties.received_time.type | string | | Mar 31, 2021 at 14:40:13 UTC |
action_result.data.\*.attributes.body.properties.reported_time.type | string | | Mar 31, 2021 at 14:40:45 UTC |
action_result.data.\*.attributes.body.properties.vision_results.type | string | | object |
action_result.data.\*.attributes.body.properties.vision_results.properties.results_id | string | | 61 |
action_result.data.\*.attributes.body.properties.vision_results.properties.query_created.type | string | | Apr 2, 2021 at 14:37:35 UTC |
action_result.data.\*.attributes.body.properties.vision_results.properties.messages_found | string | | 2 |
action_result.data.\*.attributes.body.properties.vision_results.properties.messages_removed | string | | 0 |
action_result.data.\*.attributes.body.properties.escalation_type.type | string | | |
action_result.data.\*.attributes.body.properties.malware_families.type | string | | |
action_result.data.\*.attributes.tags | string | `cofensetriage tag` | TEST |
action_result.status | string | | success failed |
action_result.message | string | | Successfully retrieved the comment |
action_result.summary | string | | |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'get rules'

Retrieve rules from the Cofense Triage Platform filtered based on the provided parameters

Type: **investigate** \
Read only: **True**

If no value is provided in any parameter, then all the records will be retrieved.

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**name** | optional | Allows filtering the rules based on the name | string | `cofensetriage rule name` |
**description** | optional | Allows filtering the rules based on the description | string | `cofensetriage rule description` |
**priority** | optional | Allows filtering the rules based on the priority | numeric | `cofensetriage priority` |
**tags** | optional | Allows filtering the rules based on the list of comma-separated tags. If the tag value contains a comma, enclose it in double-quotes (Example: tag1,"test,tag",tag2) | string | `cofensetriage tag` |
**scope** | optional | Allows filtering the rules based on the scope | string | `cofensetriage rule scope` |
**author_name** | optional | Allows filtering the rules based on the author name | string | `cofensetriage rule author name` |
**rule_context** | optional | Allows filtering the rules based on the context | string | `cofensetriage rule context` |
**active** | optional | Allows filtering the rules based on the status | boolean | |
**reports_count** | optional | Allows filtering the rules based on the number of reports the rule matched | numeric | `cofensetriage rule reports count` |
**reports_count_operator** | optional | Operator to work with the reports count parameter | string | |
**start_date** | optional | Allows filtering the rules updated on or after the provided date | string | `date` |
**end_date** | optional | Allows filtering the rules updated before the provided date | string | `date` |
**sort** | optional | Allows sorting the rules based on the 'updated_at' date of the rule | string | |
**max_results** | optional | Maximum number of results to return | numeric | |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.parameter.name | string | `cofensetriage rule name` | test |
action_result.parameter.description | string | `cofensetriage rule description` | test |
action_result.parameter.priority | numeric | `cofensetriage priority` | 1 |
action_result.parameter.tags | string | `cofensetriage tag` | test |
action_result.parameter.scope | string | `cofensetriage rule scope` | Email |
action_result.parameter.author_name | string | `cofensetriage rule author name` | author1 |
action_result.parameter.rule_context | string | `cofensetriage rule context` | Internal safe |
action_result.parameter.active | boolean | | True False |
action_result.parameter.reports_count | numeric | `cofensetriage rule reports count` | 10 |
action_result.parameter.reports_count_operator | string | | eq |
action_result.parameter.start_date | string | `date` | 2021-03-5 11:20:00 |
action_result.parameter.end_date | string | `date` | 2021-03-11 01:20:00 |
action_result.parameter.sort | string | | oldest_first latest_first |
action_result.parameter.max_results | numeric | | 5 |
action_result.data.\*.id | string | `cofensetriage rule id` | 1690 |
action_result.data.\*.type | string | | rules |
action_result.data.\*.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/rules/1690 |
action_result.data.\*.attributes.name | string | `cofensetriage rule name` | MX_Testing |
action_result.data.\*.attributes.scope | string | `cofensetriage rule scope` | Email |
action_result.data.\*.attributes.active | boolean | | True False |
action_result.data.\*.attributes.content | string | | |
action_result.data.\*.attributes.priority | numeric | `cofensetriage priority` | 5 |
action_result.data.\*.attributes.created_at | string | `date` | 2020-11-24T15:19:12.616Z |
action_result.data.\*.attributes.updated_at | string | `date` | 2020-11-24T15:19:12.616Z |
action_result.data.\*.attributes.author_name | string | `cofensetriage rule author name` | author1 |
action_result.data.\*.attributes.description | string | `cofensetriage rule description` | Test description |
action_result.data.\*.attributes.imported_at | string | | |
action_result.data.\*.attributes.rule_context | string | `cofensetriage rule context` | Phishing Tactic |
action_result.data.\*.attributes.time_to_live | string | | Forever |
action_result.data.\*.attributes.reports_count | numeric | `cofensetriage rule reports count` | 1 |
action_result.data.\*.attributes.share_with_cofense | boolean | | False True |
action_result.data.\*.relationships.owner.data.id | string | | 2 |
action_result.data.\*.relationships.owner.data.type | string | | operators |
action_result.data.\*.relationships.owner.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/rules/1690/relationships/owner |
action_result.data.\*.relationships.owner.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/rules/1690/owner |
action_result.data.\*.relationships.reports.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/rules/1690/relationships/reports |
action_result.data.\*.relationships.reports.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/rules/1690/reports |
action_result.data.\*.relationships.clusters.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/rules/1690/relationships/clusters |
action_result.data.\*.relationships.clusters.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/rules/1690/clusters |
action_result.data.\*.relationships.report_context.data | string | | |
action_result.data.\*.relationships.report_context.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/rules/1690/relationships/report_context |
action_result.data.\*.relationships.report_context.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/rules/1690/report_context |
action_result.data.\*.relationships.cluster_context.data | string | | |
action_result.data.\*.relationships.cluster_context.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/rules/1690/relationships/cluster_context |
action_result.data.\*.relationships.cluster_context.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/rules/1690/cluster_context |
action_result.data.\*.attributes.tags | string | `cofensetriage tag` | TEST |
action_result.status | string | | success failed |
action_result.message | string | | Total rules retrieved: 3 |
action_result.summary.total_rules_retrieved | numeric | | 3 |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'get rule'

Retrieve a rule from the Cofense Triage Platform for the provided rule ID

Type: **investigate** \
Read only: **True**

If the 'ingest_subfields' parameter is true, the report and the subfields together will get ingested into the container.

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**rule_id** | required | ID of the rule | numeric | `cofensetriage rule id` |
**ingest_report** | optional | Allows ingestion of the reports related to the rule into the container | boolean | |
**ingest_subfields** | optional | Allows ingestion of fields relating to the report into the container | boolean | |
**label** | optional | Allows ingestion of data into the container(s) with the provided label. The label must be valid or the action will fail. Required if 'ingest_report' or 'ingest_subfields' is set | string | |
**tenant** | optional | Allows creation of container(s) for the provided tenant ID or tenant name. The tenant must be valid or the action will fail. Required if 'ingest_report' or 'ingest_subfields' is set | string | |
**cef_mapping** | optional | JSON dictionary represented as a serialized JSON string. Each key in the dictionary is a potential key name in an artifact that is to be renamed to the value | string | |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.parameter.rule_id | numeric | `cofensetriage rule id` | 15 |
action_result.parameter.ingest_report | boolean | | True False |
action_result.parameter.ingest_subfields | boolean | | True False |
action_result.parameter.label | string | | events |
action_result.parameter.tenant | string | | default |
action_result.parameter.cef_mapping | string | | |
action_result.data.\*.id | string | `cofensetriage rule id` | 2534 |
action_result.data.\*.type | string | | rules |
action_result.data.\*.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/rules/2534 |
action_result.data.\*.reports.\*.id | string | `cofensetriage report id` | 688 |
action_result.data.\*.reports.\*.meta.risk_score_summary.vip | numeric | | 5 |
action_result.data.\*.reports.\*.meta.risk_score_summary.rules | numeric | | 1 |
action_result.data.\*.reports.\*.meta.risk_score_summary.reporter | numeric | | 15 |
action_result.data.\*.reports.\*.meta.risk_score_summary.integrations | numeric | | 2 |
action_result.data.\*.reports.\*.type | string | | reports |
action_result.data.\*.reports.\*.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/688 |
action_result.data.\*.reports.\*.attributes.md5 | string | `md5` | 8e956591920c7c49047235e7605d6838 |
action_result.data.\*.reports.\*.attributes.sha256 | string | `sha256` | 53669341f34ad3dfc467d8c1ece15e1dcf8b26a856d9228df10aaa3aa0802116 |
action_result.data.\*.reports.\*.attributes.subject | string | `cofensetriage report subject` | test |
action_result.data.\*.reports.\*.attributes.location | string | `cofensetriage report location` | Inbox |
action_result.data.\*.reports.\*.attributes.html_body | string | | |
action_result.data.\*.reports.\*.attributes.text_body | string | | |
action_result.data.\*.reports.\*.attributes.created_at | string | `date` | 2020-12-29T14:14:32.875Z |
action_result.data.\*.reports.\*.attributes.risk_score | numeric | `cofensetriage risk score` | 23 |
action_result.data.\*.reports.\*.attributes.updated_at | string | `date` | 2021-04-22T10:34:54.666Z |
action_result.data.\*.reports.\*.attributes.raw_headers | string | | |
action_result.data.\*.reports.\*.attributes.received_at | string | `date` | 2020-12-29T14:10:18.000Z |
action_result.data.\*.reports.\*.attributes.reported_at | string | `date` | 2020-12-29T14:10:16.000Z |
action_result.data.\*.reports.\*.attributes.from_address | string | `email` | test@example.com |
action_result.data.\*.reports.\*.attributes.processed_at | string | `date` | 2021-04-22T10:34:54.666Z |
action_result.data.\*.reports.\*.attributes.match_priority | numeric | `cofensetriage priority` | 1 |
action_result.data.\*.reports.\*.container_id | numeric | `container id` | 2844 |
action_result.data.\*.reports.\*.relationships.urls.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/688/relationships/urls |
action_result.data.\*.reports.\*.relationships.urls.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/688/urls |
action_result.data.\*.reports.\*.relationships.rules.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/688/relationships/rules |
action_result.data.\*.reports.\*.relationships.rules.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/688/rules |
action_result.data.\*.reports.\*.relationships.cluster.data.id | string | | 217 |
action_result.data.\*.reports.\*.relationships.cluster.data.type | string | | clusters |
action_result.data.\*.reports.\*.relationships.cluster.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/688/relationships/cluster |
action_result.data.\*.reports.\*.relationships.cluster.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/688/cluster |
action_result.data.\*.reports.\*.relationships.domains.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/688/relationships/domains |
action_result.data.\*.reports.\*.relationships.domains.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/688/domains |
action_result.data.\*.reports.\*.relationships.headers.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/688/relationships/headers |
action_result.data.\*.reports.\*.relationships.headers.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/688/headers |
action_result.data.\*.reports.\*.relationships.assignee.data | string | | |
action_result.data.\*.reports.\*.relationships.assignee.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/688/relationships/assignee |
action_result.data.\*.reports.\*.relationships.assignee.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/688/assignee |
action_result.data.\*.reports.\*.relationships.category.data | string | | |
action_result.data.\*.reports.\*.relationships.category.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/688/relationships/category |
action_result.data.\*.reports.\*.relationships.category.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/688/category |
action_result.data.\*.reports.\*.relationships.comments.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/688/relationships/comments |
action_result.data.\*.reports.\*.relationships.comments.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/688/comments |
action_result.data.\*.reports.\*.relationships.reporter.data.id | string | `cofensetriage reporter id` | 24 |
action_result.data.\*.reports.\*.relationships.reporter.data.type | string | | reporters |
action_result.data.\*.reports.\*.relationships.reporter.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/688/relationships/reporter |
action_result.data.\*.reports.\*.relationships.reporter.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/688/reporter |
action_result.data.\*.reports.\*.relationships.hostnames.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/688/relationships/hostnames |
action_result.data.\*.reports.\*.relationships.hostnames.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/688/hostnames |
action_result.data.\*.reports.\*.relationships.attachments.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/688/relationships/attachments |
action_result.data.\*.reports.\*.relationships.attachments.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/688/attachments |
action_result.data.\*.reports.\*.relationships.threat_indicators.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/688/relationships/threat_indicators |
action_result.data.\*.reports.\*.relationships.threat_indicators.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/688/threat_indicators |
action_result.data.\*.reports.\*.relationships.attachment_payloads.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/688/relationships/attachment_payloads |
action_result.data.\*.reports.\*.relationships.attachment_payloads.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/reports/688/attachment_payloads |
action_result.data.\*.attributes.name | string | `cofensetriage rule name` | test_rule1 |
action_result.data.\*.attributes.tags | string | `cofensetriage tag` | TEST |
action_result.data.\*.attributes.scope | string | `cofensetriage rule scope` | Email |
action_result.data.\*.attributes.active | boolean | | True False |
action_result.data.\*.attributes.content | string | | |
action_result.data.\*.attributes.priority | numeric | `cofensetriage priority` | 1 |
action_result.data.\*.attributes.created_at | string | `date` | 2021-04-19T10:31:44.773Z |
action_result.data.\*.attributes.updated_at | string | `date` | 2021-04-22T10:34:50.310Z |
action_result.data.\*.attributes.author_name | string | `cofensetriage rule author name` | author1 |
action_result.data.\*.attributes.description | string | `cofensetriage rule description` | Its is a test rule |
action_result.data.\*.attributes.imported_at | string | | |
action_result.data.\*.attributes.rule_context | string | `cofensetriage rule context` | Unknown |
action_result.data.\*.attributes.time_to_live | string | | Forever |
action_result.data.\*.attributes.reports_count | numeric | `cofensetriage rule reports count` | 3 |
action_result.data.\*.attributes.share_with_cofense | boolean | | False True |
action_result.data.\*.relationships.owner.data.id | string | | 9 |
action_result.data.\*.relationships.owner.data.type | string | | operators |
action_result.data.\*.relationships.owner.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/rules/2534/relationships/owner |
action_result.data.\*.relationships.owner.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/rules/2534/owner |
action_result.data.\*.relationships.reports.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/rules/2534/relationships/reports |
action_result.data.\*.relationships.reports.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/rules/2534/reports |
action_result.data.\*.relationships.clusters.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/rules/2534/relationships/clusters |
action_result.data.\*.relationships.clusters.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/rules/2534/clusters |
action_result.data.\*.relationships.report_context.data | string | | |
action_result.data.\*.relationships.report_context.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/rules/2534/relationships/report_context |
action_result.data.\*.relationships.report_context.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/rules/2534/report_context |
action_result.data.\*.relationships.cluster_context.data | string | | |
action_result.data.\*.relationships.cluster_context.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/rules/2534/relationships/cluster_context |
action_result.data.\*.relationships.cluster_context.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/rules/2534/cluster_context |
action_result.status | string | | success failed |
action_result.message | string | | Successfully retrieved the rule |
action_result.summary | string | | |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'get integration submissions'

Retrieve integration submissions from the Cofense Triage Platform filtered based on the provided parameters

Type: **investigate** \
Read only: **True**

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**type** | required | The type of integration submission | string | |
**value** | required | The value of integration submission | string | `hash` `md5` `sha256` `url` |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.parameter.type | string | | URL |
action_result.parameter.value | string | `hash` `md5` `sha256` `url` | https://test.com |
action_result.data.\*.id | string | | 158 |
action_result.data.\*.type | string | | integration_submissions |
action_result.data.\*.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/integration_submissions/158 |
action_result.data.\*.attributes.kind | string | | Hash |
action_result.data.\*.attributes.result | string | | |
action_result.data.\*.attributes.status | string | | complete |
action_result.data.\*.attributes.risk_score | numeric | `cofensetriage risk score` | 0 |
action_result.data.\*.attributes.created_at | string | `date` | 2021-04-13T15:43:59.609Z |
action_result.data.\*.attributes.updated_at | string | `date` | 2021-04-13T15:52:11.485Z |
action_result.data.\*.relationships.target.data.id | string | | 190 |
action_result.data.\*.relationships.target.data.type | string | | attachment_payloads |
action_result.data.\*.relationships.target.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/integration_submissions/158/relationships/target |
action_result.data.\*.relationships.target.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/integration_submissions/158/target |
action_result.data.\*.relationships.integration.data.id | string | | 6 |
action_result.data.\*.relationships.integration.data.type | string | | integrations |
action_result.data.\*.relationships.integration.links.self | string | `url` | https://cofensetriageurl.com/api/public/v2/integration_submissions/158/relationships/integration |
action_result.data.\*.relationships.integration.links.related | string | `url` | https://cofensetriageurl.com/api/public/v2/integration_submissions/158/integration |
action_result.status | string | | success failed |
action_result.message | string | | Total integration submissions retrieved: 1 |
action_result.summary.total_integration_submissions_retrieved | numeric | | 1 |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'on poll'

Action handler for the on poll ingest functionality

Type: **ingest** \
Read only: **True**

This action ingests reports or threat indicators from Cofense Triage as per the selected ingestion type.

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**container_count** | optional | Maximum number of containers to ingest | numeric | |
**start_time** | optional | Parameter ignored in this app | numeric | |
**end_time** | optional | Parameter ignored in this app | numeric | |
**artifact_count** | optional | Parameter ignored in this app | numeric | |

#### Action Output

No Output

______________________________________________________________________

Auto-generated Splunk SOAR Connector documentation.

Copyright 2025 Splunk Inc.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing,
software distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and limitations under the License.
