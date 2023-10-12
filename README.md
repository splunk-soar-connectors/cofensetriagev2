[comment]: # "Auto-generated SOAR connector documentation"
# Cofense Triage v2 API

Publisher: Cofense  
Connector Version: 1\.0\.4  
Product Vendor: Cofense  
Product Name: Triage v2  
Product Version Supported (regex): "\.\*"  
Minimum Product Version: 4\.9\.39220  

This app supports actions for Cofense Triage's version 2 API for faster bidirectional phishing analysis and response

[comment]: # " File: readme.md"
[comment]: # ""
[comment]: # "    Copyright (c) 2021-2023 Cofense"
[comment]: # ""
[comment]: # "    This unpublished material is proprietary to Cofense."
[comment]: # "    All rights reserved. The methods and"
[comment]: # "    techniques described herein are considered trade secrets"
[comment]: # "    and/or confidential. Reproduction or distribution, in whole"
[comment]: # "    or in part, is forbidden except by express written permission"
[comment]: # "    of Cofense."
[comment]: # ""
[comment]: # "    Licensed under Apache 2.0 (https://www.apache.org/licenses/LICENSE-2.0.txt)"
[comment]: # ""
## Explanation of the Asset Configuration Parameters

The asset configuration parameters affect \[test connectivity\] and some other actions of the
application. Below are the explanation and usage of all these parameters. The parameters related to
test connectivity action are Server URL, Verify server certificate, Client ID, and Client Secret.

-   **Server URL:** The URL used to connect with the Cofense Triage server. Example:
    https://platform.cofensetriage.com
-   **Verify server certificate:** Validate server certificate.
-   **Client ID:** Client ID.
-   **Client Secret:** Client Secret.
-   **Data to be ingested:** The type of data that is to be ingested. The following are the valid
    values:  
    -   reports
    -   threat_indicators
-   **Threat indicator type:** The type of threat indicators to retrieve. The default value is "All"
    which retrieves all types of threat indicators. The following are the valid values that the
    parameter can take:  
    -   All
    -   Header
    -   Hostname
    -   URL
    -   MD5
    -   SHA256
-   **Threat indicator level:** The level of the threat indicators to retrieve. The default value is
    "All" which retrieves all levels of threat indicators. The following are the valid values that
    the parameter can take:  
    -   All
    -   Malicious
    -   Suspicious
    -   Benign
-   **Report location:** The location of the reports to retrieve. The default value is "All" which
    retrieves reports from all the locations. The following are the valid values that the parameter
    can take:  
    -   All
    -   Inbox
    -   Reconnaissance
    -   Processed
-   **Match priority:** The highest priority of a rule matching the reported email.
-   **Category ID:** The category ID of the report.
-   **Tags:** This parameter allows filtering the reports based on the list of comma-separated tags.
    If the tag value contains a comma, enclose it in double-quotes, for example:
    tag1,"test,tag",tag2. If a comma-separated list is provided, reports matching any of the tags
    from the provided list will be retrieved.
-   **Categorization tags:** This parameter allows filtering the reports based on the list of
    comma-separated categorization tags. If a comma-separated list is provided, reports matching any
    of the tags from the provided list will be retrieved.
-   **Ingest subfields:** Whether or not to ingest the subfields of the selected data. If this
    parameter is set to true, the data and all the resources related to the data that are present in
    the relationships will be ingested.
-   **Category ID to severity mapping:** The mapping in JSON format between the category ID of the
    report and the Phantom container severity. If no value is provided, then the default mapping
    will be used and, if the category ID isn't present in the default mapping the severity will be
    set to "Low". If a value is provided, the combination of the provided value and the default
    mapping will be used to decide the severity. The default mapping is: {"High": \["4"\], "Medium":
    \["3"\], "Low": \["1", "2", "5"\]}. Example value for the parameter is: {"High": \["8", "9"\],
    "Medium": \["7"\], "Low": \["6"\]}
-   **Cef mapping:** This parameter is a JSON dictionary represented as a serialized JSON string.
    Each key in the dictionary is a potential key name in an artifact that is to be renamed to the
    value. For example, if the cef_mapping is {"website":"requestURL"} your artifact will have
    requestURL cef field in place of website cef field. This parameter will be taken into
    consideration only during ingestion.
-   **Start date:** The initial start date and time of the ingestion. This parameter retrieves the
    data that was updated on or after the provided date. It will be taken into consideration during
    the poll now and the first run of scheduled/interval polling.
-   **Sort:** This parameter allows sorting the data based on the 'updated_at' date. The default
    value is "oldest_first" which sorts the results in the oldest first order. The following are the
    valid values that the parameter can take:  
    -   oldest_first
    -   latest_first
-   **Update state after:** This parameter saves the context after ingestion of every provided
    number of containers. This parameter is only used for scheduled/interval polling and only if the
    sort parameter value is "oldest_first".
-   **Max results:** Maximum number of results to ingest. If not provided all the data will be
    ingested.

## Explanation of the Actions' Parameters

-   ### Test Connectivity (Action Workflow Details)

    -   This action will test the connectivity of the Phantom server to the Cofense Triage instance
        by making an initial API call using the provided asset configuration parameters. This action
        can be used to generate a new token.
    -   The action validates the provided asset configuration parameters. Based on the API call
        response, the appropriate success and failure message will be displayed when the action gets
        executed.

-   ### Get reports

    -   **<u>Action Parameter:</u> Location**

          

        -   This parameter allows filtering the reports based on the location. The following are the
            valid values that the parameter can take:  
            -   All
            -   Inbox
            -   Reconnaissance
            -   Processed

    -   **<u>Action Parameter:</u> From address**

          

        -   This parameter allows filtering the reports based on the sender's email address of the
            reported email.

    -   **<u>Action Parameter:</u> Reporter's email**

          

        -   This parameter allows filtering the reports based on the reporter's email address of the
            reported email.

    -   **<u>Action Parameter:</u> Subject**

          

        -   This parameter allows filtering the reports with the subject containing a specific
            string. All the reports containing the provided value in the subject will be retrieved.

    -   **<u>Action Parameter:</u> Match priority**

          

        -   This parameter allows filtering the reports based on the highest priority of a rule
            matching the reported email.

    -   **<u>Action Parameter:</u> Category ID**

          

        -   This parameter allows filtering the reports based on the category ID of the report.

    -   **<u>Action Parameter:</u> Start date**

          

        -   This parameter allows filtering the reports updated on or after the provided date.

    -   **<u>Action Parameter:</u> End date**

          

        -   This parameter allows filtering the reports updated before the provided date.

    -   **<u>Action Parameter:</u> Tags**

          

        -   This parameter allows filtering the reports based on the list of comma-separated tags.
            If the tag value contains a comma, enclose it in double-quotes, for example:
            tag1,"test,tag",tag2. If a comma-separated list is provided, reports matching any of the
            tags from the provided list will be retrieved.

    -   **<u>Action Parameter:</u> Categorization tags**

          

        -   This parameter allows filtering the reports based on the list of comma-separated
            categorization tags. If a comma-separated list is provided, reports matching any of the
            tags from the provided list will be retrieved.

    -   **<u>Action Parameter:</u> Sort**

          

        -   This parameter allows sorting the reports based on the 'updated_at' date of the report.
            By default, it will sort in the oldest first order. The following are the valid values
            that the parameter can take:  
            -   oldest_first
            -   latest_first

    -   **<u>Action Parameter:</u> Ingest report**

          

        -   This parameter allows the ingestion of the report into the container.

    -   **<u>Action Parameter:</u> Ingest subfields**

          

        -   This parameter allows the ingestion of the fields relating to the report into the
            container. If this parameter is set to true, the report and all the resources related to
            the report that are present in the relationships together will get ingested into the
            container.

    -   **<u>Action Parameter:</u> Label**

          

        -   This parameter allows the ingestion of data into the container(s) with the provided
            label. The label must be valid or the action will fail. Required if 'ingest_report' or
            'ingest_subfields' is set. This parameter will be taken into consideration only during
            ingestion.

    -   **<u>Action Parameter:</u> Tenant**

          

        -   This parameter allows the creation of container(s) for the provided tenant ID or tenant
            name. The tenant must be valid or the action will fail. Required if 'ingest_report' or
            'ingest_subfields' is set. This parameter will be taken into consideration only during
            ingestion.

    -   **<u>Action Parameter:</u> Cef mapping**

          

        -   This parameter is a JSON dictionary represented as a serialized JSON string. Each key in
            the dictionary is a potential key name in an artifact that is to be renamed to the
            value. For example, if the cef_mapping is {"website":"requestURL"} your artifact will
            have requestURL cef field in place of website cef field. This parameter will be taken
            into consideration only during ingestion.

    -   **<u>Action Parameter:</u> Max results**

          

        -   Maximum number of results to return. If not provided all the data will be retrieved.

    -   **Note -** If no value is provided in any parameter, then all the records will be retrieved.

    -   **Example:**
        -   List all the reports present in Inbox containing “demo” word in the subject and having
            match priority equals 5 and is sent by 'abc@test.com'.
            -   Location = Inbox
            -   Subject = Demo
            -   Match Priority = 5
            -   From Address = abc@test.com
        -   List all the reports updated between 2020-09-23T08:31:58Z and 2020-09-29T09:00:00Z and
            sort them in oldest_first order.
            -   Start date = 2020-09-23T08:31:58Z
            -   End date = 2020-09-29T09:00:00Z
            -   Sort = oldest_first
        -   List the reports in the latest_first order.
            -   Sort = latest_first

-   ### Get report

    -   **<u>Action Parameter:</u> Report ID**

          

        -   The ID of the report to be retrieved.

    -   **<u>Action Parameter:</u> Ingest report**

          

        -   This parameter allows the ingestion of the report into the container.

    -   **<u>Action Parameter:</u> Ingest subfields**

          

        -   This parameter allows the ingestion of the fields relating to the report into the
            container. If this parameter is set to true, the report and all the resources related to
            the report that are present in the relationships together will get ingested into the
            container.

    -   **<u>Action Parameter:</u> Label**

          

        -   This parameter allows the ingestion of data into the container(s) with the provided
            label. The label must be valid or the action will fail. Required if 'ingest_report' or
            'ingest_subfields' is set. This parameter will be taken into consideration only during
            ingestion.

    -   **<u>Action Parameter:</u> Tenant**

          

        -   This parameter allows the creation of container(s) for the provided tenant ID or tenant
            name. The tenant must be valid or the action will fail. Required if 'ingest_report' or
            'ingest_subfields' is set. This parameter will be taken into consideration only during
            ingestion.

    -   **<u>Action Parameter:</u> Cef mapping**

          

        -   This parameter is a JSON dictionary represented as a serialized JSON string. Each key in
            the dictionary is a potential key name in an artifact that is to be renamed to the
            value. For example, if the cef_mapping is {"website":"requestURL"} your artifact will
            have requestURL cef field in place of website cef field. This parameter will be taken
            into consideration only during ingestion.

    -   **Example:**
        -   Fetch the report with ID equals 15.
            -   Report ID = 15

-   ### Categorize report

    -   **<u>Action Parameter:</u> Report ID**

          

        -   This parameter is the ID of the report which the user wants to categorize.

    -   **<u>Action Parameter:</u> Category ID**

          

        -   This parameter is the ID of the category into which the user wants to categorize the
            report. Category ID is either known by Cofense Triage users or it can be fetched from
            the output of Get categories action.

    -   **<u>Action Parameter:</u> Category Name**

          

        -   This parameter is the name of the category into which the user wants to categorize the
            report. This parameter can be provided if the category ID is not known by Cofense Triage
            users.

    -   **<u>Action Parameter:</u> Response ID**

          

        -   This parameter is the ID of the response.

    -   **<u>Action Parameter:</u> Categorization Tags**

          

        -   This parameter allows the user to provide multiple tags to be given to the report while
            categorizing it. It accepts a comma-separated list of tags.

    -   **Note -** If both category ID and category name are provided, then category ID will be
        given a higher priority.

    -   **Example:**
        -   Categorize the report having Report ID 5, with given category ID 1, and add
            categorization tag ‘test’.
            -   Report ID = 5
            -   Category ID = 1
            -   Categorization tags = test
        -   Categorize the report having Report ID 10, with given category ID 2 and add
            categorization tag ‘test tag’, also send a response using response template ID 2.
            -   Report ID = 10
            -   Category ID = 2
            -   Categorization tags = test tag
            -   Response ID = 2

-   ### Get reporters

    -   **<u>Action Parameter:</u> VIP**

          

        -   This parameter allows searching for the VIP reporters. If the value of the parameter is
            false, then all the reporters will be retrieved.

    -   **<u>Action Parameter:</u> Reputation score**

          

        -   This parameter allows searching for reporters having the provided reputation score. It
            allows a comma-separated list. If a comma-separated list is provided, then the reporters
            with any of the specified scores will be retrieved.

    -   **<u>Action Parameter:</u> Email**

          

        -   This parameter allows searching for the reporter with a specific email.

    -   **<u>Action Parameter:</u> Sort**

          

        -   This parameter allows sorting the reporters based on the ID. By default, it will sort in
            the oldest first order. The following are the valid values that the parameter can
            take:  
            -   oldest_first
            -   latest_first

    -   **<u>Action Parameter:</u> Max results**

          

        -   Maximum number of results to return. If not provided, all the data will be retrieved.

    -   **Note -** If no value is provided in any parameter, then all the records will be retrieved.

    -   **Example:**
        -   List the latest 15 VIP reporters with a reputation score equals 15.
            -   VIP = true
            -   Reputation Score = 15
            -   Max results = 15
            -   Sort = latest_first
        -   Fetch the reporter with the email address abc@test.com.
            -   Email = abc@test.com

-   ### Get reporter

    -   **<u>Action Parameter:</u> Reporter ID**

          

        -   This parameter is the ID of the reporter to fetch.

    -   **Example:**
        -   Fetch the reporter with the Reporter ID equals 10.
            -   Report ID = 10

-   ### Get URLs

    -   **<u>Action Parameter:</u> Risk score**

          

        -   This parameter is the risk score of the URL.

    -   **<u>Action Parameter:</u> Risk score operator**

          

        -   This parameter is the operator to work with the risk score parameter. The default value
            is 'eq'.For example: if the risk score = 5 and the risk score operator = 'lt', then all
            the URLs having a risk score less than 5 will be retrieved. The following are the valid
            values that the parameter can take:  
            -   eq
            -   not_eq
            -   lt
            -   lteq
            -   gt
            -   gteq

    -   **<u>Action Parameter:</u> URL Value**

          

        -   This parameter is the value of the URL to search for.

    -   **<u>Action Parameter:</u> Start date**

          

        -   This parameter allows filtering the URLs updated on or after the provided date.

    -   **<u>Action Parameter:</u> End date**

          

        -   This parameter allows filtering the URLs updated before the provided date.

    -   **<u>Action Parameter:</u> Sort**

          

        -   This parameter allows sorting the URLs based on the 'updated_at' date of the URL. By
            default, it will sort in the oldest first order. The following are the valid values that
            the parameter can take:  
            -   oldest_first
            -   latest_first

    -   **<u>Action Parameter:</u> Max results**

          

        -   Maximum number of results to return. If not provided, all the data will be retrieved.

    -   **Note -** If no value is provided in any parameter, then all the records will be retrieved.

    -   **Example:**
        -   List all the URLs having a risk score equals 5 in the latest first order.
            -   Risk score ID = 5
            -   Risk score operator = eq
            -   Sort = latest_first
        -   List the URL having value equals 'https://testurl.com'.
            -   URL value = https://testurl.com
        -   List oldest 5 URLs that are updated between 2020-09-23T08:31:58Z and
            2020-09-29T09:00:00Z.
            -   Start date = 2020-09-23T08:31:58Z
            -   End date = 2020-09-29T09:00:00Z
            -   Sort = oldest_first
            -   Max results = 5

-   ### Get url

    -   **<u>Action Parameter:</u> URL ID**

          

        -   This parameter is the ID of the URL to fetch.

    -   **Example:**
        -   Fetch the URL with URL ID equals 5.
            -   URL ID = 5

-   ### Create response

    -   **<u>Action Parameter:</u> Name**

          

        -   This parameter specifies a short display name of the response sent to individuals when a
            report is categorized.

    -   **<u>Action Parameter:</u> Description**

          

        -   This parameter specifies the expanded name or description of the response.

    -   **<u>Action Parameter:</u> Subject**

          

        -   This parameter specifies the subject of the response. It supports template variables.

    -   **<u>Action Parameter:</u> Body**

          

        -   This parameter specifies the body of the email. It supports template variables.

    -   **<u>Action Parameter:</u> To reporter**

          

        -   This parameter specifies whether to add the reporter to the response recipient list
            (true) or not (false). The default is true. Either 'to_reporter' or 'to_other', or both,
            must be enabled.

    -   **<u>Action Parameter:</u> To other**

          

        -   This parameter specifies whether to add the addresses specified in 'to_other_address' to
            the response recipient list (true) or not (false). The default is false. If true,
            specify one or more values in 'to_other_address'. Either to_reporter or 'to_other', or
            both, must be enabled.

    -   **<u>Action Parameter:</u> To other address**

          

        -   This parameter is a comma-separated list of email addresses to send the response to.
            Works with 'to_other'.

    -   **<u>Action Parameter:</u> Attach original**

          

        -   This parameter specifies whether to attach the original email to the response (true) or
            not (false).

    -   **<u>Action Parameter:</u> CC address**

          

        -   This parameter is a comma-separated list of email addresses to CC the response to.

    -   **<u>Action Parameter:</u> BCC address**

          

        -   This parameter is a comma-separated list of email addresses to BCC the response to.

    -   **Template variables:** The user can insert variables into the subject and body of the
        response while creating it. When the response is sent as a result of categorizing a report,
        Cofense Triage replaces the variables with information from that report. The following are
        the template variables

          

        -   \[SUBJECT\]: Replaced with the subject of the reported email.
        -   \[REPORT_DATE\]: Replaced with the date the email was reported.

    -   **Example:**
        -   Create a response with name: "Example Response", Description: "This is an example
            response", Subject: "Email '\[SUBJECT\]' reported \[REPORT_DATE\] is SAFE", and Body =
            "The email '\[SUBJECT\]' that you reported on \[REPORT_DATE\] is safe".
            -   Name = Example Response
            -   Description = This is an example response
            -   Subject = Email '\[SUBJECT\]' reported \[REPORT_DATE\] is SAFE
            -   Body = The email '\[SUBJECT\]' that you reported on \[REPORT_DATE\] is safe
        -   Create a response with name: "Example Response", Subject: "Email '\[SUBJECT\]' reported
            \[REPORT_DATE\] is SAFE", and Body = "The email '\[SUBJECT\]' that you reported on
            \[REPORT_DATE\] is safe". The response should be sent to the reporter and not others.
            -   Name = Example Response
            -   To reporter = true
            -   To other = false
            -   Subject = Email '\[SUBJECT\]' reported \[REPORT_DATE\] is SAFE
            -   Body = The email '\[SUBJECT\]' that you reported on \[REPORT_DATE\] is safe

    **Note:** This action is supported for Cofense Triage with version older than 1.23.

-   ### Get responses

    -   **<u>Action Parameter:</u> Max results**

          

        -   This parameter allows the user to limit the number of results. It expects a numeric
            value as an input.

    -   **Example:**
        -   List 50 responses.
            -   Max results = 50

    **Note:** This action is supported for Cofense Triage with version older than 1.23.

-   ### Create threat indicator

    -   **<u>Action Parameter:</u> Level**

          

        -   This parameter is the level of threat indicator. The following are the valid values that
            the parameter can take:  
            -   Malicious
            -   Suspicious
            -   Benign

    -   **<u>Action Parameter:</u> Type**

          

        -   This parameter is the type of threat indicator. The following are the valid values that
            the parameter can take:  
            -   Header
            -   Hostname
            -   URL
            -   MD5
            -   SHA256

    -   **<u>Action Parameter:</u> Value**

          

        -   This parameter is the value of the threat indicator. If the value of the parameter
            'type' is 'Header', then the value of this parameter should be in the form
            {header_key}:{header_value}.

    -   **<u>Action Parameter:</u> Source**

          

        -   This parameter is the source of the threat indicator. The default value of this
            parameter is "Splunk_Phantom-UI"

    -   **Example:**
        -   Create a malicious threat indicator with type: URL and value: 'https://testurl.com'.
            -   Level = Malicious
            -   Type = URL
            -   Value = 'https://testurl.com'
        -   Create a Suspicious threat indicator, source: 'Splunk_Phantom-UI', type: Header and
            value: 'From:test@test.com'
            -   Level = Suspicious
            -   Type = Header
            -   Value = From:test@test.com
            -   Source = Splunk_Phantom-UI

-   ### Get categories

    -   **<u>Action Parameter:</u> Name**

          

        -   This parameter allows the user to fetch the categories with the name containing a
            specific string.

    -   **<u>Action Parameter:</u> Malicious**

          

        -   This parameter allows the user to fetch the categories based on whether the category is
            used to classify malicious reports or not. If the value is false, then all the
            categories will be fetched.

    -   **<u>Action Parameter:</u> Max results**

          

        -   Maximum number of results to return. If not provided, all the data will be retrieved.

    -   **Note -** If no value is provided in any parameter, then all the records will be retrieved.

    -   **Example:**
        -   List the categories containing ‘threat’ in the name and are malicious.
            -   Name = Threat
            -   Malicious = true
        -   List 50 categories.
            -   Max results = 50

-   ### Get threat indicators

    -   **<u>Action Parameter:</u> Level**

          

        -   This parameter allows filtering based on the level of threat indicator. The following
            are the valid values that the parameter can take:  
            -   All
            -   Malicious
            -   Suspicious
            -   Benign

    -   **<u>Action Parameter:</u> Type**

          

        -   This parameter allows filtering based on the type of threat indicator. The following are
            the valid values that the parameter can take:  
            -   All
            -   Header
            -   Hostname
            -   URL
            -   MD5
            -   SHA256

    -   **<u>Action Parameter:</u> Source**

          

        -   This parameter allows filtering based on the source of the threat. If not provided,
            threat indicators from all the sources will be fetched.

    -   **<u>Action Parameter:</u> Value**

          

        -   This parameter allows filtering based on the actual value of the threat indicator.

    -   **<u>Action Parameter:</u> Start date**

          

        -   This parameter allows the user to fetch the threat indicators updated on or after the
            provided date.

    -   **<u>Action Parameter:</u> End date**

          

        -   This parameter allows the user to fetch the threat indicators updated before the
            provided date.

    -   **<u>Action Parameter:</u> Sort**

          

        -   This parameter allows sorting the result data set based on the 'updated_at' date of the
            threat indicator. By default, it will sort in the oldest first order. The following are
            the valid values that the parameter can take:  
            -   oldest_first
            -   latest_first

    -   **<u>Action Parameter:</u> Ingest threat indicator**

          

        -   This parameter allows ingestion of the threat indicator(s) into the container(s).

    -   **<u>Action Parameter:</u> Ingest subfields**

          

        -   This parameter allows the ingestion of the fields relating to the threat indicator into
            the container. If this parameter is set to true, the threat indicator and all the
            resources related to the threat indicator that are present in the relationships together
            will get ingested.

    -   **<u>Action Parameter:</u> Label**

          

        -   This parameter allows the ingestion of data into the container(s) with the provided
            label. The label must be valid or the action will fail. Required if
            'ingest_threat_indicator' or 'ingest_subfields' is set. This parameter will be taken
            into consideration only during ingestion.

    -   **<u>Action Parameter:</u> Tenant**

          

        -   This parameter allows the creation of container(s) for the provided tenant ID or tenant
            name. The tenant must be valid or the action will fail. Required if
            'ingest_threat_indicator' or 'ingest_subfields' is set. This parameter will be taken
            into consideration only during ingestion.

    -   **<u>Action Parameter:</u> Cef mapping**

          

        -   This parameter is a JSON dictionary represented as a serialized JSON string. Each key in
            the dictionary is a potential key name in an artifact that is to be renamed to the
            value. For example, if the cef_mapping is {"website":"requestURL"} your artifact will
            have requestURL cef field in place of website cef field. This parameter will be taken
            into consideration only during ingestion.

    -   **<u>Action Parameter:</u> Max results**

          

        -   Maximum number of results to return. If not provided all the data will be retrieved.

    -   **Note -** If no value is provided in any parameter then all the records will be retrieved.

    -   **Example:**
        -   List all the Malicious threat indicators that are URLs and are reported from the
            Triage-UI source.
            -   Level = Malicious
            -   Type = URL
            -   Source = Triage-UI
        -   List all the threat indicators updated between 2020-09-23T08:31:58Z and
            2020-09-29T09:00:00Z and sort them in oldest_first order.
            -   Start date = 2020-09-23T08:31:58Z
            -   End date = 2020-09-29T09:00:00Z
            -   Sort = oldest_first
        -   List 50 threat indicators in the latest first order.
            -   Max results = 50
            -   Sort = latest_first

-   ### Get email

    -   **<u>Action Parameter:</u> Report ID**

          

        -   This parameter is the ID of the report.

    -   **<u>Action Parameter:</u> Download method**

          

        -   This parameter allows the user to download the email as an artifact or as a vaulted
            file.

    -   **<u>Action Parameter:</u> Create vaulted file artifact**

          

        -   If storing the file as a vaulted file, this parameter allows the user to create an
            artifact referencing that file.

    -   **Example:**
        -   Download email for report ID equals 10.
            -   Report ID = 10
            -   Download method = vaulted file

-   ### Get Comments

    -   **<u>Action Parameter:</u> Body format**

          

        -   This parameter allows filtering the comments based on the body format. The following are
            the valid values that the parameter can take:  
            -   all
            -   text
            -   json

    -   **<u>Action Parameter:</u> Tags**

          

        -   This parameter allows filtering the comments based on the list of comma-separated tags.
            If the tag value contains a comma, enclose it in double-quotes, for example:
            tag1,"test,tag",tag2. If a comma-separated list is provided, comments matching any of
            the tags from the provided list will be retrieved.

    -   **<u>Action Parameter:</u> Start date**

          

        -   This parameter allows filtering the comments updated on or after the provided date.

    -   **<u>Action Parameter:</u> End date**

          

        -   This parameter allows filtering the comments updated before the provided date.

    -   **<u>Action Parameter:</u> Sort**

          

        -   This parameter allows sorting the comments based on the 'updated_at' date of the
            comment. By default, it will sort in the oldest first order. The following are the valid
            values that the parameter can take:  
            -   oldest_first
            -   latest_first

    -   **<u>Action Parameter:</u> Max results**

          

        -   Maximum number of results to return. If not provided, all the data will be retrieved.

    -   **Note -** If no value is provided in any parameter, then all the records will be retrieved.

    -   **Example:**
        -   List the latest 20 comments having 'text' body format with a tag 'test'.
            -   Body format = text
            -   Tags = test
            -   Sort = latest_first
            -   Max results = 20
        -   List all the comments updated between 2020-09-23T08:31:58Z and 2020-09-29T09:00:00Z and
            sort them in oldest_first order.
            -   Start date = 2020-09-23T08:31:58Z
            -   End date = 2020-09-29T09:00:00Z
            -   Sort = oldest_first
        -   List the comments in the latest_first order.
            -   Sort = latest_first

-   ### Get comment

    -   **<u>Action Parameter:</u> Comment ID**

          

        -   This parameter is the ID of the comment to fetch.

    -   **Example:**
        -   Fetch the comment with comment ID equals 5.
            -   Comment ID = 5

-   ### Get rule

    -   **<u>Action Parameter:</u> Rule ID**

          

        -   This parameter is the ID of the rule to fetch.

    -   **<u>Action Parameter:</u> Ingest report**

          

        -   This parameter allows ingestion of reports related to the rule.

    -   **<u>Action Parameter:</u> Ingest subfields**

          

        -   This parameter allows the ingestion of the fields relating to the report into the
            container. If this parameter is set to true, the report and all the resources related to
            the report that are present in the relationships together will get ingested into the
            container.

    -   **<u>Action Parameter:</u> Label**

          

        -   This parameter allows the ingestion of data into the container(s) with the provided
            label. The label must be valid or the action will fail. Required if 'ingest_report' or
            'ingest_subfields' is set. This parameter will be taken into consideration only during
            ingestion.

    -   **<u>Action Parameter:</u> Tenant**

          

        -   This parameter allows the creation of container(s) for the provided tenant ID or tenant
            name. The tenant must be valid or the action will fail. Required if 'ingest_report' or
            'ingest_subfields' is set. This parameter will be taken into consideration only during
            ingestion.

    -   **<u>Action Parameter:</u> Cef mapping**

          

        -   This parameter is a JSON dictionary represented as a serialized JSON string. Each key in
            the dictionary is a potential key name in an artifact that is to be renamed to the
            value. For example, if the cef_mapping is {"website":"requestURL"} your artifact will
            have requestURL cef field in place of website cef field. This parameter will be taken
            into consideration only during ingestion.

    -   **Example:**
        -   Fetch the rule with rule ID equals 5 and ingest the reports related to the rule.
            -   Rule ID = 5
            -   Ingest reports = True
            -   Label = events
            -   Tenant = Default

-   ### Get rules

    -   **<u>Action Parameter:</u> Name**

          

        -   This parameter allows filtering the rules with rule name containing a specific string.
            All the rules containing the provided value in the name will be retrieved.

    -   **<u>Action Parameter:</u> Description**

          

        -   This parameter allows filtering the rules with rule description containing a specific
            string. All the rules containing the provided value in the description will be
            retrieved.

    -   **<u>Action Parameter:</u> Priority**

          

        -   This parameter allows filtering the rules based on the priority.

    -   **<u>Action Parameter:</u> Tags**

          

        -   This parameter allows filtering the rules based on the list of comma-separated tags. If
            the tag value contains a comma, enclose it in double-quotes, for example:
            tag1,"test,tag",tag2. If a comma-separated list is provided, rules matching any of the
            tags from the provided list will be retrieved.

    -   **<u>Action Parameter:</u> Scope**

          

        -   This parameter allows filtering the rules based on the scope.

    -   **<u>Action Parameter:</u> Author name**

          

        -   This parameter allows filtering the rules with author name containing a specific string.
            All the rules containing the provided value in the author's name will be retrieved.

    -   **<u>Action Parameter:</u> Rule context**

          

        -   This parameter allows filtering the rules based on the context. The following are the
            valid values that the parameter can take:  
            -   All
            -   Internal safe
            -   Unwanted
            -   Threat hunting
            -   Phishing tactic
            -   Cleanup
            -   Unknown

    -   **<u>Action Parameter:</u> Active**

          

        -   This parameter allows filtering the rules based on the status. If the value of the
            parameter is false, then all the rules will be retrieved.

    -   **<u>Action Parameter:</u> Reports count**

          

        -   This parameter allows filtering the rules based on the number of reports the rule
            matched.

    -   **<u>Action Parameter:</u> Reports count operator**

          

        -   This parameter is the operator to work with the reports count parameter. The default
            value is 'eq'. For example: if the reports count = 5 and the reports count operator =
            'lt', then all the rules having a report count less than 5 will be retrieved. The
            following are the valid values that the parameter can take:  
            -   eq
            -   not_eq
            -   lt
            -   lteq
            -   gt
            -   gteq

    -   **<u>Action Parameter:</u> Start date**

          

        -   This parameter allows filtering the rules updated on or after the provided date.

    -   **<u>Action Parameter:</u> End date**

          

        -   This parameter allows filtering the rules updated before the provided date.

    -   **<u>Action Parameter:</u> Sort**

          

        -   This parameter allows sorting the rules based on the 'updated_at' date. By default, it
            will sort in the oldest first order. The following are the valid values that the
            parameter can take:  
            -   oldest_first
            -   latest_first

    -   **<u>Action Parameter:</u> Max results**

          

        -   Maximum number of results to return. If not provided all the data will be retrieved.

    -   **Note -** If no value is provided in any parameter, then all the records will be retrieved.

    -   **Example:**
        -   Fetch the active rules created by 'author1' with name equals 'test' having tag equals
            'test' and priority equals 1.
            -   Name = test
            -   Priority = 1
            -   Author name = author1
            -   Active = True
            -   Tags = test
        -   List all the rules updated between 2020-09-23T08:31:58Z and 2020-09-29T09:00:00Z and
            sort them in oldest_first order.
            -   Start date = 2020-09-23T08:31:58Z
            -   End date = 2020-09-29T09:00:00Z
            -   Sort = oldest_first
        -   Fetch 20 rules with report count equals 5.
            -   Reports count = 5
            -   Reports count operator = eq
            -   Max results = 20

-   ### Get integration submissions

    -   **<u>Action Parameter:</u> Type**

          

        -   This parameter is the type of integration submission.

    -   **<u>Action Parameter:</u> Value**

          

        -   This parameter is the value of integration submission.

    -   **Example:**
        -   List integration submissions of type MD5 with value equals
            f033362ca459dcab56aa6b2274751d13.
            -   Type = MD5
            -   Value = f033362ca459dcab56aa6b2274751d13
        -   List integration submissions of type URL with value equals http://test.com.
            -   Type = URL
            -   Value = http://test.com

-   ### On Poll

    -   ### What is On Poll

        -   It will ingest data from the external system into the phantom server in the form of
            containers and artifacts. There are two approaches to polling which are mentioned below.

              

            -   POLL NOW (Manual polling)

                  

                -   It will fetch the data every time as per the corresponding asset configuration
                    parameters. It doesn’t store the last run context of the fetched data. The
                    corresponding asset configuration parameters for the POLL NOW are
                    ingestion_type, threat_indicator_type, threat_indicator_level, report_location,
                    match_priority, category_id, tags, categorization_tags, ingest_subfields,
                    category_id_to_severity, cef_mapping, start_date, sort and max_results.

            -   Scheduled/Interval Polling

                  

                -   Scheduled Polling: The ingestion action can be triggered at every specified
                    timestamp interval.
                -   Interval Polling: The ingestion action can be triggered at every time range
                    interval.
                -   It will fetch the data every time as per the corresponding asset configuration
                    parameters based on the stored context from the previous ingestion run. It
                    stores the last run context of the fetched data. It starts fetching data based
                    on the combination of the values of stored context for the previous ingestion
                    run and the corresponding asset configuration parameters. The corresponding
                    asset configuration parameters for the scheduled/interval are ingestion_type,
                    threat_indicator_type, threat_indicator_level, report_location, match_priority,
                    category_id, tags, categorization_tags, ingest_subfields,
                    category_id_to_severity, cef_mapping, start_date, sort, update_state_after and
                    max_results.

    -   ### Containers and Artifacts creation

        -   We have configured two types of data ingestion which you can select from the asset
            configuration parameters. Below are the two types

              

            -   reports: It will ingest only the reports.
            -   threat_indicators: It will ingest only the threat indicators.

        -   Container

              

            -   A container is a composite object that consists of one or more artifacts that can be
                automated. Containers are the top-level data structure that Playbooks operate on.
                Every container has a common header, and beneath that, the ability to store
                arbitrary less structured JSON.

        -   Artifacts

              

            -   Artifacts are objects that are associated with a Container and serve as
                corroboration or evidence related to the Container.

        -   Each report or threat indicator will be ingested as an artifact in a separate container.
            Each subfield related to the report or the threat indicator will get ingested into the
            container of that report or threat indicator as a separate artifact if the
            'ingest_subfields' parameter is true. Below is the explanation based on the type of data
            for that.

              

            -   **reports**

                  
                    For this type, one container will be created for each report.

                -   Container 1:- Subject of the report

                      

                    -   This container will be used to store fetched report data in the form of
                        artifacts.

            -   **threat indicators**

                  
                    For this type, one container will be created for each threat indicator.

                -   Container 1:- Threat Indicator ID - ID

                      

                    -   This container will be used to store fetched threat indicator data in the
                        form of artifacts.

    -   ### Stored Context

        -   It is the concept of storing the context of the previous ingestion run. This concept
            will be used in the scheduled/interval polling. It will use the state file to store the
            last run context. This state file will be created for the created asset for the
            application on the phantom platform.

              

            -   State file location:

                  

                -   For non-NRI Instances:
                    /opt/phantom/local_data/app_states/7129d563-a28d-4afc-8081-f909dce54293
                -   For NRI Instances:
                    /home/phanru/phantomcyber/local_data/app_states/7129d563-a28d-4afc-8081-f909dce54293

            -   The default format of state file: {"app_version": "1.0.0"}

    -   **Example:**
        -   Ingest the Malicious threat indicators that are URLs and are updated on or after
            2020-09-23T08:31:58Z.
            -   Ingestion type = threat_indicators
            -   Threat Indicator Level = Malicious
            -   Threat Indicator Type = URL
            -   Start date = 2020-09-23T08:31:58Z
        -   Ingest the reports present in Inbox having match priority equals 5 and are updated on or
            after 2020-09-23T08:31:58Z.
            -   Ingestion type = reports
            -   Report Location = Inbox
            -   Match Priority = 5
            -   Start date = 2020-09-23T08:31:58Z


### Configuration Variables
The below configuration variables are required for this Connector to operate.  These variables are specified when configuring a Triage v2 asset in SOAR.

VARIABLE | REQUIRED | TYPE | DESCRIPTION
-------- | -------- | ---- | -----------
**base\_url** |  required  | string | Server URL
**verify\_server\_cert** |  optional  | boolean | Verify server certificate
**client\_id** |  required  | string | Client ID
**client\_secret** |  required  | password | Client Secret
**ingestion\_type** |  optional  | string | The type of data that is to be ingested
**threat\_indicator\_type** |  optional  | string | Filters the results based on the type of the threat indicator\. The default retrieves all
**threat\_indicator\_level** |  optional  | string | Filters the results based on the level of the threat indicator\. The default retrieves all
**report\_location** |  optional  | string | Filters the reports based on the location of the report\. The default retrieves all
**match\_priority** |  optional  | numeric | Filters the results based on the highest priority of a rule matching the reported email
**category\_id** |  optional  | numeric | Filters the reports based on the category ID
**tags** |  optional  | string | Allows filtering the reports based on the list of comma\-separated tags
**categorization\_tags** |  optional  | string | Allows filtering the reports based on the list of comma\-separated categorization tags
**ingest\_subfields** |  optional  | boolean | Allows ingestion of the fields relating to the fetched data into the container
**category\_id\_to\_severity** |  optional  | string | Mapping between report category ID and the Phantom container severity
**cef\_mapping** |  optional  | string | JSON dictionary represented as a serialized JSON string\. Each key in the dictionary is a potential key name in an artifact that is to be renamed to the value
**start\_date** |  optional  | string | The initial start date and time of the ingestion
**sort** |  optional  | string | Sorts the results based on the 'updated\_at' date\. The default sorts in the oldest first order
**update\_state\_after** |  optional  | numeric | Allows updating the state after ingestion of a specified number of containers
**max\_results** |  optional  | numeric | Maximum number of results to ingest

### Supported Actions  
[test connectivity](#action-test-connectivity) - Validate the asset configuration for connectivity using supplied configuration  
[get reports](#action-get-reports) - Retrieve reports from the Cofense Triage Platform filtered based on the provided parameters  
[get report](#action-get-report) - Retrieve a report with the provided ID from the Cofense Triage Platform  
[get email](#action-get-email) - Downloads the raw email for the report that matches the specified report ID  
[get categories](#action-get-categories) - Retrieve categories from the Cofense Triage Platform filtered based on the provided parameters  
[get responses](#action-get-responses) - Retrieve responses from the Cofense Triage Platform\. This action is supported for Cofense Triage with version older than 1\.23  
[create response](#action-create-response) - Create a response\. This action is supported for Cofense Triage with version older than 1\.23  
[categorize report](#action-categorize-report) - Categorize a report into the provided category  
[get threat indicators](#action-get-threat-indicators) - Retrieve threat indicators from the Cofense Triage Platform filtered based on the provided parameters  
[create threat indicator](#action-create-threat-indicator) - Create a threat indicator with the provided parameters  
[get reporters](#action-get-reporters) - Retrieve reporters from the Cofense Triage Platform filtered based on the provided parameters  
[get reporter](#action-get-reporter) - Retrieve a reporter from the Cofense Triage Platform for the provided reporter ID  
[get urls](#action-get-urls) - Retrieve URLs from the Cofense Triage Platform filtered based on the provided parameters  
[get url](#action-get-url) - Retrieve a URL from the Cofense Triage Platform for the provided URL ID  
[get comments](#action-get-comments) - Retrieve comments from the Cofense Triage Platform filtered based on the provided parameters  
[get comment](#action-get-comment) - Retrieve a comment from the Cofense Triage Platform for the provided comment ID  
[get rules](#action-get-rules) - Retrieve rules from the Cofense Triage Platform filtered based on the provided parameters  
[get rule](#action-get-rule) - Retrieve a rule from the Cofense Triage Platform for the provided rule ID  
[get integration submissions](#action-get-integration-submissions) - Retrieve integration submissions from the Cofense Triage Platform filtered based on the provided parameters  
[on poll](#action-on-poll) - Action handler for the on poll ingest functionality  

## action: 'test connectivity'
Validate the asset configuration for connectivity using supplied configuration

Type: **test**  
Read only: **True**

#### Action Parameters
No parameters are required for this action

#### Action Output
No Output  

## action: 'get reports'
Retrieve reports from the Cofense Triage Platform filtered based on the provided parameters

Type: **investigate**  
Read only: **True**

If the 'ingest\_subfields' parameter is true, the report and the subfields together will get ingested into the container\. If no value is provided in any parameter, then all the records will be retrieved\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**location** |  optional  | Allows filtering the reports based on the location | string |  `cofensetriage report location` 
**from\_address** |  optional  | Allows filtering the reports based on the sender's email address of the reported email | string |  `email` 
**reporter\_email** |  optional  | Allows filtering the reports based on the reporter's email address | string |  `email` 
**subject** |  optional  | Allows filtering the reports based on the subject of the reported email | string |  `cofensetriage report subject` 
**match\_priority** |  optional  | Allows filtering the result data set based on the highest priority of a rule matching the reported email | numeric |  `cofensetriage priority` 
**category\_id** |  optional  | Allows filtering the reports based on the category ID | numeric |  `cofensetriage category id` 
**start\_date** |  optional  | Allows filtering the reports updated on or after the provided date | string |  `date` 
**end\_date** |  optional  | Allows filtering the reports updated before the provided date | string |  `date` 
**tags** |  optional  | Allows filtering the reports based on the list of comma\-separated tags\. If the tag value contains a comma, enclose it in double\-quotes \(Example\: tag1,"test,tag",tag2\) | string |  `cofensetriage tag` 
**categorization\_tags** |  optional  | Allows filtering the reports based on the list of comma\-separated categorization tags | string |  `cofensetriage tag` 
**sort** |  optional  | Allows sorting the reports based on the 'updated\_at' date of the report | string | 
**ingest\_report** |  optional  | Allows ingestion of the report into the container | boolean | 
**ingest\_subfields** |  optional  | Allows ingestion of the fields relating to the report into the container | boolean | 
**label** |  optional  | Allows ingestion of data into the container\(s\) with the provided label\. The label must be valid or the action will fail\. Required if 'ingest\_report' or 'ingest\_subfields' is set | string | 
**tenant** |  optional  | Allows creation of container\(s\) for the provided tenant ID or tenant name\. The tenant must be valid or the action will fail\. Required if 'ingest\_report' or 'ingest\_subfields' is set | string | 
**cef\_mapping** |  optional  | JSON dictionary represented as a serialized JSON string\. Each key in the dictionary is a potential key name in an artifact that is to be renamed to the value | string | 
**max\_results** |  optional  | Maximum number of results to return | numeric | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.location | string |  `cofensetriage report location` 
action\_result\.parameter\.from\_address | string |  `email` 
action\_result\.parameter\.reporter\_email | string |  `email` 
action\_result\.parameter\.subject | string |  `cofensetriage report subject` 
action\_result\.parameter\.match\_priority | numeric |  `cofensetriage priority` 
action\_result\.parameter\.category\_id | numeric |  `cofensetriage category id` 
action\_result\.parameter\.start\_date | string |  `date` 
action\_result\.parameter\.end\_date | string |  `date` 
action\_result\.parameter\.tags | string |  `cofensetriage tag` 
action\_result\.parameter\.categorization\_tags | string |  `cofensetriage tag` 
action\_result\.parameter\.sort | string | 
action\_result\.parameter\.ingest\_report | boolean | 
action\_result\.parameter\.ingest\_subfields | boolean | 
action\_result\.parameter\.label | string | 
action\_result\.parameter\.tenant | string | 
action\_result\.parameter\.cef\_mapping | string | 
action\_result\.parameter\.max\_results | numeric | 
action\_result\.data\.\*\.id | string |  `cofensetriage report id` 
action\_result\.data\.\*\.meta\.risk\_score\_summary\.vip | numeric | 
action\_result\.data\.\*\.meta\.risk\_score\_summary\.rules | numeric | 
action\_result\.data\.\*\.meta\.risk\_score\_summary\.reporter | numeric | 
action\_result\.data\.\*\.meta\.risk\_score\_summary\.integrations | numeric | 
action\_result\.data\.\*\.type | string | 
action\_result\.data\.\*\.links\.self | string |  `url` 
action\_result\.data\.\*\.attributes\.md5 | string |  `md5` 
action\_result\.data\.\*\.attributes\.sha256 | string |  `sha256` 
action\_result\.data\.\*\.attributes\.subject | string |  `cofensetriage report subject` 
action\_result\.data\.\*\.attributes\.location | string |  `cofensetriage report location` 
action\_result\.data\.\*\.attributes\.html\_body | string | 
action\_result\.data\.\*\.attributes\.text\_body | string | 
action\_result\.data\.\*\.attributes\.created\_at | string |  `date` 
action\_result\.data\.\*\.attributes\.risk\_score | numeric | 
action\_result\.data\.\*\.attributes\.updated\_at | string |  `date` 
action\_result\.data\.\*\.attributes\.raw\_headers | string | 
action\_result\.data\.\*\.attributes\.received\_at | string |  `date` 
action\_result\.data\.\*\.attributes\.reported\_at | string |  `date` 
action\_result\.data\.\*\.attributes\.from\_address | string |  `email` 
action\_result\.data\.\*\.attributes\.processed\_at | string |  `date` 
action\_result\.data\.\*\.attributes\.match\_priority | numeric |  `cofensetriage priority` 
action\_result\.data\.\*\.attributes\.categorization\_tags | string |  `cofensetriage tag` 
action\_result\.data\.\*\.attributes\.tags | string |  `cofensetriage tag` 
action\_result\.data\.\*\.container\_id | numeric |  `container id` 
action\_result\.data\.\*\.relationships\.urls\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.urls\.links\.related | string |  `url` 
action\_result\.data\.\*\.relationships\.rules\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.rules\.links\.related | string |  `url` 
action\_result\.data\.\*\.relationships\.cluster\.data\.id | string | 
action\_result\.data\.\*\.relationships\.cluster\.data\.type | string | 
action\_result\.data\.\*\.relationships\.cluster\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.cluster\.links\.related | string |  `url` 
action\_result\.data\.\*\.relationships\.headers\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.headers\.links\.related | string |  `url` 
action\_result\.data\.\*\.relationships\.assignee\.data\.id | string | 
action\_result\.data\.\*\.relationships\.assignee\.data\.type | string | 
action\_result\.data\.\*\.relationships\.assignee\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.assignee\.links\.related | string |  `url` 
action\_result\.data\.\*\.relationships\.category\.data\.id | string |  `cofensetriage category id` 
action\_result\.data\.\*\.relationships\.category\.data\.type | string | 
action\_result\.data\.\*\.relationships\.category\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.category\.links\.related | string |  `url` 
action\_result\.data\.\*\.relationships\.reporter\.data\.id | string |  `cofensetriage reporter id` 
action\_result\.data\.\*\.relationships\.reporter\.data\.type | string | 
action\_result\.data\.\*\.relationships\.reporter\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.reporter\.links\.related | string |  `url` 
action\_result\.data\.\*\.relationships\.hostnames\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.hostnames\.links\.related | string |  `url` 
action\_result\.data\.\*\.relationships\.attachments\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.attachments\.links\.related | string |  `url` 
action\_result\.data\.\*\.relationships\.threat\_indicators\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.threat\_indicators\.links\.related | string |  `url` 
action\_result\.data\.\*\.relationships\.attachment\_payloads\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.attachment\_payloads\.links\.related | string |  `url` 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
action\_result\.summary\.total\_reports\_retrieved | numeric | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'get report'
Retrieve a report with the provided ID from the Cofense Triage Platform

Type: **investigate**  
Read only: **True**

If the 'ingest\_subfields' parameter is true, the report and the subfields together will get ingested into the container\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**report\_id** |  required  | The ID of the report which is to be fetched | numeric |  `cofensetriage report id` 
**ingest\_report** |  optional  | Allow ingestion of the report into the container | boolean | 
**ingest\_subfields** |  optional  | Ingestion of the fields relating to the report into the container | boolean | 
**label** |  optional  | Allows ingestion of data into the container\(s\) with the provided label\. The label must be valid or the action will fail\. Required if 'ingest\_report' or 'ingest\_subfields' is set | string | 
**tenant** |  optional  | Allows creation of container\(s\) for the provided tenant ID or tenant name\. The tenant must be valid or the action will fail\. Required if 'ingest\_report' or 'ingest\_subfields' is set | string | 
**cef\_mapping** |  optional  | JSON dictionary represented as a serialized JSON string\. Each key in the dictionary is a potential key name in an artifact that is to be renamed to the value | string | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.report\_id | numeric |  `cofensetriage report id` 
action\_result\.parameter\.ingest\_report | boolean | 
action\_result\.parameter\.ingest\_subfields | boolean | 
action\_result\.parameter\.label | string | 
action\_result\.parameter\.tenant | string | 
action\_result\.parameter\.cef\_mapping | string | 
action\_result\.data\.\*\.id | string |  `cofensetriage report id` 
action\_result\.data\.\*\.container\_id | numeric |  `container id` 
action\_result\.data\.\*\.meta\.risk\_score\_summary\.vip | numeric | 
action\_result\.data\.\*\.meta\.risk\_score\_summary\.rules | numeric | 
action\_result\.data\.\*\.meta\.risk\_score\_summary\.reporter | numeric | 
action\_result\.data\.\*\.meta\.risk\_score\_summary\.integrations | numeric | 
action\_result\.data\.\*\.type | string | 
action\_result\.data\.\*\.links\.self | string |  `url` 
action\_result\.data\.\*\.attributes\.md5 | string |  `md5` 
action\_result\.data\.\*\.attributes\.sha256 | string |  `sha256` 
action\_result\.data\.\*\.attributes\.subject | string |  `cofensetriage report subject` 
action\_result\.data\.\*\.attributes\.location | string |  `cofensetriage report location` 
action\_result\.data\.\*\.attributes\.html\_body | string | 
action\_result\.data\.\*\.attributes\.text\_body | string | 
action\_result\.data\.\*\.attributes\.created\_at | string |  `date` 
action\_result\.data\.\*\.attributes\.risk\_score | numeric | 
action\_result\.data\.\*\.attributes\.updated\_at | string |  `date` 
action\_result\.data\.\*\.attributes\.raw\_headers | string | 
action\_result\.data\.\*\.attributes\.received\_at | string |  `date` 
action\_result\.data\.\*\.attributes\.reported\_at | string |  `date` 
action\_result\.data\.\*\.attributes\.from\_address | string |  `email` 
action\_result\.data\.\*\.attributes\.processed\_at | string |  `date` 
action\_result\.data\.\*\.attributes\.match\_priority | numeric |  `cofensetriage priority` 
action\_result\.data\.\*\.attributes\.categorization\_tags | string |  `cofensetriage tag` 
action\_result\.data\.\*\.attributes\.tags | string |  `cofensetriage tag` 
action\_result\.data\.\*\.relationships\.urls\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.urls\.links\.related | string |  `url` 
action\_result\.data\.\*\.relationships\.rules\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.rules\.links\.related | string |  `url` 
action\_result\.data\.\*\.relationships\.cluster\.data\.id | string | 
action\_result\.data\.\*\.relationships\.cluster\.data\.type | string | 
action\_result\.data\.\*\.relationships\.cluster\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.cluster\.links\.related | string |  `url` 
action\_result\.data\.\*\.relationships\.headers\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.headers\.links\.related | string |  `url` 
action\_result\.data\.\*\.relationships\.assignee\.data\.id | string | 
action\_result\.data\.\*\.relationships\.assignee\.data\.type | string | 
action\_result\.data\.\*\.relationships\.assignee\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.assignee\.links\.related | string |  `url` 
action\_result\.data\.\*\.relationships\.category\.data\.id | string |  `cofensetriage category id` 
action\_result\.data\.\*\.relationships\.category\.data\.type | string | 
action\_result\.data\.\*\.relationships\.category\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.category\.links\.related | string |  `url` 
action\_result\.data\.\*\.relationships\.reporter\.data\.id | string |  `cofensetriage reporter id` 
action\_result\.data\.\*\.relationships\.reporter\.data\.type | string | 
action\_result\.data\.\*\.relationships\.reporter\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.reporter\.links\.related | string |  `url` 
action\_result\.data\.\*\.relationships\.hostnames\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.hostnames\.links\.related | string |  `url` 
action\_result\.data\.\*\.relationships\.attachments\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.attachments\.links\.related | string |  `url` 
action\_result\.data\.\*\.relationships\.threat\_indicators\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.threat\_indicators\.links\.related | string |  `url` 
action\_result\.data\.\*\.relationships\.attachment\_payloads\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.attachment\_payloads\.links\.related | string |  `url` 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'get email'
Downloads the raw email for the report that matches the specified report ID

Type: **investigate**  
Read only: **True**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**report\_id** |  required  | The ID of the report | numeric |  `cofensetriage report id` 
**download\_method** |  required  | Allows the user to download the email as an artifact or as a vaulted file | string | 
**create\_vaulted\_file\_artifact** |  optional  | If storing as a vaulted file, this parameter allows the user to create an artifact referencing that file | boolean | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.create\_vaulted\_file\_artifact | boolean | 
action\_result\.parameter\.download\_method | string | 
action\_result\.parameter\.report\_id | numeric |  `cofensetriage report id` 
action\_result\.data\.\*\.artifact\_id | string |  `artifact id` 
action\_result\.data\.\*\.filename | string |  `file name` 
action\_result\.data\.\*\.md5 | string |  `md5`  `hash` 
action\_result\.data\.\*\.report\_id | string |  `cofensetriage report id` 
action\_result\.data\.\*\.sha1 | string |  `sha1`  `hash` 
action\_result\.data\.\*\.sha256 | string |  `sha256`  `hash` 
action\_result\.data\.\*\.size | string | 
action\_result\.data\.\*\.vault\_id | string |  `vault id` 
action\_result\.data\.\*\.vaulted | string |  `file path` 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary\.filename | string |  `file name` 
action\_result\.summary\.vault\_id | string |  `vault id` 
action\_result\.summary\.report\_id | numeric |  `cofensetriage report id` 
action\_result\.summary\.artifact\_id | numeric |  `artifact id` 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'get categories'
Retrieve categories from the Cofense Triage Platform filtered based on the provided parameters

Type: **investigate**  
Read only: **True**

If no value is provided in any parameter, then all the records will be retrieved\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**name** |  optional  | Allows the user to fetch the categories with the name containing a specific string | string |  `cofensetriage category name` 
**malicious** |  optional  | Allows the user to fetch the categories based on whether the category is used to classify malicious reports or not | boolean | 
**max\_results** |  optional  | Maximum number of results to return | numeric | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.name | string |  `cofensetriage category name` 
action\_result\.parameter\.malicious | boolean | 
action\_result\.parameter\.max\_results | numeric | 
action\_result\.data\.\*\.id | string |  `cofensetriage category id` 
action\_result\.data\.\*\.type | string | 
action\_result\.data\.\*\.links\.self | string |  `url` 
action\_result\.data\.\*\.attributes\.name | string |  `cofensetriage category name` 
action\_result\.data\.\*\.attributes\.color | string | 
action\_result\.data\.\*\.attributes\.score | numeric | 
action\_result\.data\.\*\.attributes\.archived | boolean | 
action\_result\.data\.\*\.attributes\.malicious | boolean | 
action\_result\.data\.\*\.attributes\.created\_at | string |  `date` 
action\_result\.data\.\*\.attributes\.updated\_at | string |  `date` 
action\_result\.data\.\*\.relationships\.reports\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.reports\.links\.related | string |  `url` 
action\_result\.data\.\*\.relationships\.one\_clicks\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.one\_clicks\.links\.related | string |  `url` 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary\.total\_categories\_retrieved | numeric | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'get responses'
Retrieve responses from the Cofense Triage Platform\. This action is supported for Cofense Triage with version older than 1\.23

Type: **investigate**  
Read only: **True**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**max\_results** |  optional  | Allows the user to limit the number of results | numeric | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.max\_results | numeric | 
action\_result\.data\.\*\.id | string |  `cofensetirage response id` 
action\_result\.data\.\*\.relationships\.one\_clicks\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.one\_clicks\.links\.related | string |  `url` 
action\_result\.data\.\*\.attributes\.body | string | 
action\_result\.data\.\*\.attributes\.name | string | 
action\_result\.data\.\*\.attributes\.to\_other | boolean | 
action\_result\.data\.\*\.attributes\.created\_at | string |  `date` 
action\_result\.data\.\*\.attributes\.updated\_at | string |  `date` 
action\_result\.data\.\*\.attributes\.bcc\_address | string |  `email` 
action\_result\.data\.\*\.attributes\.cc\_address | string |  `email` 
action\_result\.data\.\*\.attributes\.attach\_original | boolean | 
action\_result\.data\.\*\.attributes\.to\_other\_address | string |  `email` 
action\_result\.data\.\*\.attributes\.subject | string | 
action\_result\.data\.\*\.attributes\.to\_reporter | boolean | 
action\_result\.data\.\*\.attributes\.description | string | 
action\_result\.data\.\*\.type | string | 
action\_result\.data\.\*\.links\.self | string |  `url` 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary\.total\_responses\_retrieved | numeric | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'create response'
Create a response\. This action is supported for Cofense Triage with version older than 1\.23

Type: **generic**  
Read only: **False**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**name** |  required  | Display name of the response sent to individuals | string | 
**subject** |  required  | Subject of the response | string | 
**body** |  required  | Body of the email | string | 
**description** |  optional  | Description of the response | string | 
**to\_reporter** |  optional  | To add the reporter to the response recipient list or not | boolean | 
**to\_other** |  optional  | To add the addresses specified in 'to\_other\_address' to the response recipient list or not | boolean | 
**to\_other\_address** |  optional  | Comma\-separated list of email addresses to send the response to | string |  `email` 
**attach\_original** |  optional  | To attach the original email to the response or not | boolean | 
**cc\_address** |  optional  | Comma\-separated list of email addresses to CC the response to | string |  `email` 
**bcc\_address** |  optional  | Comma\-separated list of email addresses to BCC the response to | string |  `email` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.name | string | 
action\_result\.parameter\.subject | string | 
action\_result\.parameter\.body | string | 
action\_result\.parameter\.description | string | 
action\_result\.parameter\.to\_reporter | boolean | 
action\_result\.parameter\.to\_other | boolean | 
action\_result\.parameter\.to\_other\_address | string |  `email` 
action\_result\.parameter\.attach\_original | boolean | 
action\_result\.parameter\.cc\_address | string |  `email` 
action\_result\.parameter\.bcc\_address | string |  `email` 
action\_result\.data\.\*\.id | string |  `cofensetirage response id` 
action\_result\.data\.\*\.relationships\.one\_clicks\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.one\_clicks\.links\.related | string |  `url` 
action\_result\.data\.\*\.attributes\.body | string | 
action\_result\.data\.\*\.attributes\.name | string | 
action\_result\.data\.\*\.attributes\.to\_other | boolean | 
action\_result\.data\.\*\.attributes\.created\_at | string |  `date` 
action\_result\.data\.\*\.attributes\.updated\_at | string |  `date` 
action\_result\.data\.\*\.attributes\.bcc\_address | string |  `email` 
action\_result\.data\.\*\.attributes\.cc\_address | string |  `email` 
action\_result\.data\.\*\.attributes\.attach\_original | boolean | 
action\_result\.data\.\*\.attributes\.to\_other\_address | string |  `email` 
action\_result\.data\.\*\.attributes\.subject | string | 
action\_result\.data\.\*\.attributes\.to\_reporter | boolean | 
action\_result\.data\.\*\.attributes\.description | string | 
action\_result\.data\.\*\.type | string | 
action\_result\.data\.\*\.links\.self | string |  `url` 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary\.response\_id | string |  `cofensetirage response id` 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'categorize report'
Categorize a report into the provided category

Type: **generic**  
Read only: **False**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**report\_id** |  required  | The ID of the report | numeric |  `cofensetriage report id` 
**category\_id** |  optional  | The ID of the category | numeric |  `cofensetriage category id` 
**category\_name** |  optional  | The name of the category | string |  `cofensetriage category name` 
**response\_id** |  optional  | The ID of the response | numeric | 
**categorization\_tags** |  optional  | Allows the user to provide multiple tags to the report while categorizing it | string |  `cofensetriage tag` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.report\_id | numeric |  `cofensetriage report id` 
action\_result\.parameter\.response\_id | numeric | 
action\_result\.parameter\.category\_name | string |  `cofensetriage category name` 
action\_result\.parameter\.category\_id | numeric |  `cofensetriage category id` 
action\_result\.parameter\.categorization\_tags | string |  `cofensetriage tag` 
action\_result\.data | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'get threat indicators'
Retrieve threat indicators from the Cofense Triage Platform filtered based on the provided parameters

Type: **investigate**  
Read only: **True**

If the 'ingest\_subfields' parameter is true, the threat indicator and the subfields together will get ingested into the container\. If no value is provided in any parameter, then all the records will be retrieved\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**level** |  optional  | The level of the threat indicator | string |  `cofensetriage threat indicator level` 
**type** |  optional  | Type of the threat indicators | string |  `cofensetriage threat indicator type` 
**source** |  optional  | Source of the threat indicators | string |  `cofensetriage threat indicator source` 
**value** |  optional  | Value of the threat indicators | string |  `sha256`  `md5`  `url`  `hash`  `domain`  `host name` 
**start\_date** |  optional  | Threat indicators updated on or after the provided date | string |  `date` 
**end\_date** |  optional  | Threat indicators updated before the provided date | string |  `date` 
**sort** |  optional  | Sorting based on updated date of threat indicators | string | 
**ingest\_threat\_indicator** |  optional  | Ingestion of threat indicator\(s\) into the container\(s\) | boolean | 
**ingest\_subfields** |  optional  | Allow ingestion of the fields relating to the threat indicator into the container | boolean | 
**label** |  optional  | Allows ingestion of data into the container\(s\) with the provided label\. The label must be valid or the action will fail\. Required if 'ingest\_threat\_indicator' or 'ingest\_subfields' is set | string | 
**tenant** |  optional  | Allows creation of container\(s\) for the provided tenant ID or tenant name\. The tenant must be valid or the action will fail\. Required if 'ingest\_threat\_indicator' or 'ingest\_subfields' is set | string | 
**cef\_mapping** |  optional  | JSON dictionary represented as a serialized JSON string | string | 
**max\_results** |  optional  | Maximum number of results to return | numeric | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.level | string |  `cofensetriage threat indicator level` 
action\_result\.parameter\.type | string |  `cofensetriage threat indicator type` 
action\_result\.parameter\.source | string |  `cofensetriage threat indicator source` 
action\_result\.parameter\.value | string |  `sha256`  `md5`  `url`  `hash`  `domain`  `host name` 
action\_result\.parameter\.start\_date | string |  `date` 
action\_result\.parameter\.end\_date | string |  `date` 
action\_result\.parameter\.sort | string | 
action\_result\.parameter\.ingest\_threat\_indicator | string | 
action\_result\.parameter\.ingest\_subfields | string | 
action\_result\.parameter\.label | string | 
action\_result\.parameter\.tenant | string | 
action\_result\.parameter\.cef\_mapping | string | 
action\_result\.parameter\.max\_results | string | 
action\_result\.data\.\*\.id | string |  `cofensetriage threat indicator id` 
action\_result\.data\.\*\.type | string | 
action\_result\.data\.\*\.links\.self | string |  `url` 
action\_result\.data\.\*\.attributes\.created\_at | string |  `date` 
action\_result\.data\.\*\.attributes\.updated\_at | string |  `date` 
action\_result\.data\.\*\.attributes\.threat\_type | string |  `cofensetriage threat indicator type` 
action\_result\.data\.\*\.attributes\.threat\_level | string |  `cofensetriage threat indicator level` 
action\_result\.data\.\*\.attributes\.threat\_value | string |  `sha256`  `md5`  `url`  `hash`  `domain`  `host name` 
action\_result\.data\.\*\.attributes\.threat\_source | string |  `cofensetriage threat indicator source` 
action\_result\.data\.\*\.relationships\.owner\.data\.id | string | 
action\_result\.data\.\*\.relationships\.owner\.data\.type | string | 
action\_result\.data\.\*\.relationships\.owner\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.owner\.links\.related | string |  `url` 
action\_result\.data\.\*\.relationships\.reports\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.reports\.links\.related | string |  `url` 
action\_result\.data\.\*\.relationships\.comments\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.comments\.links\.related | string |  `url` 
action\_result\.data\.\*\.container\_id | numeric |  `container id` 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary\.total\_threat\_indicators\_retrieved | numeric | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'create threat indicator'
Create a threat indicator with the provided parameters

Type: **generic**  
Read only: **False**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**level** |  required  | The level of the threat indicator | string |  `cofensetriage threat indicator level` 
**type** |  required  | Type of the threat indicator | string |  `cofensetriage threat indicator type` 
**value** |  required  | Value of the threat indicator | string |  `sha256`  `md5`  `url`  `hostname`  `domain`  `hash` 
**source** |  optional  | Source of the threat indicator | string |  `cofensetriage threat indicator source` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.level | string |  `cofensetriage threat indicator level` 
action\_result\.parameter\.type | string |  `cofensetriage threat indicator type` 
action\_result\.parameter\.value | string |  `sha256`  `md5`  `url`  `hostname`  `domain`  `hash` 
action\_result\.parameter\.source | string |  `cofensetriage threat indicator source` 
action\_result\.data\.\*\.id | string |  `cofensetriage threat indicator id` 
action\_result\.data\.\*\.type | string | 
action\_result\.data\.\*\.links\.self | string |  `url` 
action\_result\.data\.\*\.attributes\.created\_at | string |  `date` 
action\_result\.data\.\*\.attributes\.updated\_at | string |  `date` 
action\_result\.data\.\*\.attributes\.threat\_type | string |  `cofensetriage threat indicator type` 
action\_result\.data\.\*\.attributes\.threat\_level | string |  `cofensetriage threat indicator level` 
action\_result\.data\.\*\.attributes\.threat\_value | string |  `sha256`  `md5`  `url`  `hostname`  `hash`  `domain` 
action\_result\.data\.\*\.attributes\.threat\_source | string |  `cofensetriage threat indicator source` 
action\_result\.data\.\*\.relationships\.owner\.data\.id | string | 
action\_result\.data\.\*\.relationships\.owner\.data\.type | string | 
action\_result\.data\.\*\.relationships\.owner\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.owner\.links\.related | string |  `url` 
action\_result\.data\.\*\.relationships\.reports\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.reports\.links\.related | string |  `url` 
action\_result\.data\.\*\.relationships\.comments\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.comments\.links\.related | string |  `url` 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary\.threat\_indicator\_id | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'get reporters'
Retrieve reporters from the Cofense Triage Platform filtered based on the provided parameters

Type: **investigate**  
Read only: **True**

If no value is provided in any parameter, then all the records will be retrieved\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**vip** |  optional  | Allows searching for the VIP reporters | boolean | 
**reputation\_score** |  optional  | Allows searching for reporters having the provided reputation score\. It allows a comma\-separated list | string |  `cofensetriage reporter reputation score` 
**email** |  optional  | Allows searching for the reporter with a specific email | string |  `email` 
**sort** |  optional  | Allows sorting the reporters based on the ID | string | 
**max\_results** |  optional  | Maximum number of results to return | numeric | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.vip | boolean | 
action\_result\.parameter\.reputation\_score | string |  `cofensetriage reporter reputation score` 
action\_result\.parameter\.email | string |  `email` 
action\_result\.parameter\.sort | string | 
action\_result\.parameter\.max\_results | numeric | 
action\_result\.data\.\*\.id | string |  `cofensetriage reporter id` 
action\_result\.data\.\*\.type | string | 
action\_result\.data\.\*\.links\.self | string |  `url` 
action\_result\.data\.\*\.attributes\.vip | boolean | 
action\_result\.data\.\*\.attributes\.email | string |  `email` 
action\_result\.data\.\*\.attributes\.created\_at | string |  `date` 
action\_result\.data\.\*\.attributes\.updated\_at | string |  `date` 
action\_result\.data\.\*\.attributes\.reports\_count | numeric | 
action\_result\.data\.\*\.attributes\.last\_reported\_at | string |  `date` 
action\_result\.data\.\*\.attributes\.reputation\_score | numeric |  `cofensetriage reporter reputation score` 
action\_result\.data\.\*\.relationships\.reports\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.reports\.links\.related | string |  `url` 
action\_result\.data\.\*\.relationships\.clusters\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.clusters\.links\.related | string |  `url` 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary\.total\_reporters\_retrieved | numeric | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'get reporter'
Retrieve a reporter from the Cofense Triage Platform for the provided reporter ID

Type: **investigate**  
Read only: **True**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**reporter\_id** |  required  | The unique ID of the reporter | numeric |  `cofensetriage reporter id` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.reporter\_id | numeric |  `cofensetriage reporter id` 
action\_result\.data\.\*\.id | string |  `cofensetriage reporter id` 
action\_result\.data\.\*\.type | string | 
action\_result\.data\.\*\.links\.self | string |  `url` 
action\_result\.data\.\*\.attributes\.vip | boolean | 
action\_result\.data\.\*\.attributes\.email | string |  `email` 
action\_result\.data\.\*\.attributes\.created\_at | string |  `date` 
action\_result\.data\.\*\.attributes\.updated\_at | string |  `date` 
action\_result\.data\.\*\.attributes\.reports\_count | numeric | 
action\_result\.data\.\*\.attributes\.last\_reported\_at | string |  `date` 
action\_result\.data\.\*\.attributes\.reputation\_score | numeric |  `cofensetriage reporter reputation score` 
action\_result\.data\.\*\.relationships\.reports\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.reports\.links\.related | string |  `url` 
action\_result\.data\.\*\.relationships\.clusters\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.clusters\.links\.related | string |  `url` 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'get urls'
Retrieve URLs from the Cofense Triage Platform filtered based on the provided parameters

Type: **investigate**  
Read only: **True**

If no value is provided in any parameter, then all the records will be retrieved\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**risk\_score** |  optional  | Risk score of the URL | numeric |  `cofensetriage risk score` 
**risk\_score\_operator** |  optional  | Operator to work with the risk score parameter | string | 
**url\_value** |  optional  | Value of the URL to search for | string |  `url` 
**start\_date** |  optional  | Allows filtering the URLs updated on or after the provided date | string |  `date` 
**end\_date** |  optional  | Allows filtering the URLs updated before the provided date | string |  `date` 
**sort** |  optional  | Allows sorting the URLs based on the 'updated\_at' date | string | 
**max\_results** |  optional  | Maximum number of results to return | numeric | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.risk\_score | numeric |  `cofensetriage risk score` 
action\_result\.parameter\.risk\_score\_operator | string | 
action\_result\.parameter\.url\_value | string |  `url` 
action\_result\.parameter\.start\_date | string |  `date` 
action\_result\.parameter\.end\_date | string |  `date` 
action\_result\.parameter\.sort | string | 
action\_result\.parameter\.max\_results | numeric | 
action\_result\.data\.\*\.id | string |  `cofensetriage url id` 
action\_result\.data\.\*\.type | string | 
action\_result\.data\.\*\.links\.self | string |  `url` 
action\_result\.data\.\*\.attributes\.url | string |  `url` 
action\_result\.data\.\*\.attributes\.created\_at | string |  `date` 
action\_result\.data\.\*\.attributes\.risk\_score | string |  `cofensetriage risk score` 
action\_result\.data\.\*\.attributes\.updated\_at | string |  `date` 
action\_result\.data\.\*\.relationships\.reports\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.reports\.links\.related | string |  `url` 
action\_result\.data\.\*\.relationships\.clusters\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.clusters\.links\.related | string |  `url` 
action\_result\.data\.\*\.relationships\.hostname\.data\.id | string | 
action\_result\.data\.\*\.relationships\.hostname\.data\.type | string | 
action\_result\.data\.\*\.relationships\.hostname\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.hostname\.links\.related | string |  `url` 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary\.total\_urls\_retrieved | numeric | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'get url'
Retrieve a URL from the Cofense Triage Platform for the provided URL ID

Type: **investigate**  
Read only: **True**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**url\_id** |  required  | ID of the URL | numeric |  `cofensetriage url id` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.url\_id | numeric |  `cofensetriage url id` 
action\_result\.data\.\*\.id | string |  `cofensetriage url id` 
action\_result\.data\.\*\.type | string | 
action\_result\.data\.\*\.links\.self | string |  `url` 
action\_result\.data\.\*\.attributes\.url | string |  `url` 
action\_result\.data\.\*\.attributes\.created\_at | string |  `date` 
action\_result\.data\.\*\.attributes\.risk\_score | string |  `cofensetriage risk score` 
action\_result\.data\.\*\.attributes\.updated\_at | string |  `date` 
action\_result\.data\.\*\.relationships\.reports\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.reports\.links\.related | string |  `url` 
action\_result\.data\.\*\.relationships\.clusters\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.clusters\.links\.related | string |  `url` 
action\_result\.data\.\*\.relationships\.hostname\.data\.id | string | 
action\_result\.data\.\*\.relationships\.hostname\.data\.type | string | 
action\_result\.data\.\*\.relationships\.hostname\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.hostname\.links\.related | string |  `url` 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'get comments'
Retrieve comments from the Cofense Triage Platform filtered based on the provided parameters

Type: **investigate**  
Read only: **True**

If no value is provided in any parameter, then all the records will be retrieved\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**body\_format** |  optional  | Allows filtering the comments based on the format of the comment body | string |  `cofensetriage comment body format` 
**tags** |  optional  | Allows filtering the comments based on the list of comma\-separated tags\. If the tag value contains a comma, enclose it in double\-quotes \(Example\: tag1,"test,tag",tag2\) | string |  `cofensetriage tag` 
**start\_date** |  optional  | Allows filtering the comments updated on or after the provided date | string |  `date` 
**end\_date** |  optional  | Allows filtering the comments updated before the provided date | string |  `date` 
**sort** |  optional  | Allows sorting the comments based on the 'updated\_at' date of the comment | string | 
**max\_results** |  optional  | Maximum number of results to return | numeric | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.body\_format | string |  `cofensetriage comment body format` 
action\_result\.parameter\.tags | string |  `cofensetriage tag` 
action\_result\.parameter\.start\_date | string |  `date` 
action\_result\.parameter\.end\_date | string |  `date` 
action\_result\.parameter\.sort | string | 
action\_result\.parameter\.max\_results | numeric | 
action\_result\.data\.\*\.id | string |  `cofensetriage comment id` 
action\_result\.data\.\*\.type | string | 
action\_result\.data\.\*\.links\.self | string |  `url` 
action\_result\.data\.\*\.attributes\.body | string | 
action\_result\.data\.\*\.attributes\.created\_at | string |  `date` 
action\_result\.data\.\*\.attributes\.updated\_at | string |  `date` 
action\_result\.data\.\*\.attributes\.body\_format | string |  `cofensetriage comment body format` 
action\_result\.data\.\*\.relationships\.owner\.data\.id | string | 
action\_result\.data\.\*\.relationships\.owner\.data\.type | string | 
action\_result\.data\.\*\.relationships\.owner\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.owner\.links\.related | string |  `url` 
action\_result\.data\.\*\.relationships\.commentable\.data\.id | string | 
action\_result\.data\.\*\.relationships\.commentable\.data\.type | string | 
action\_result\.data\.\*\.relationships\.commentable\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.commentable\.links\.related | string |  `url` 
action\_result\.data\.\*\.attributes\.body\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.from\.type | string |  `email` 
action\_result\.data\.\*\.attributes\.body\.properties\.notes\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.brands\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.brands\.items\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.srctag\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.sent\_to\.type | string |  `email` 
action\_result\.data\.\*\.attributes\.body\.properties\.subject\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.summary\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.reply\_to\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.report\_id\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.message\_id\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.phenotypes\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.report\_url\.type | string |  `url` 
action\_result\.data\.\*\.attributes\.body\.properties\.reported\_by\.type | string |  `email` 
action\_result\.data\.\*\.attributes\.body\.properties\.stage\_1\_iocs\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.stage\_1\_iocs\.properties\.files\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.stage\_1\_iocs\.properties\.infection\_ips\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.stage\_1\_iocs\.properties\.infection\_ips\.items\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.stage\_1\_iocs\.properties\.infection\_urls\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.stage\_1\_iocs\.properties\.infection\_urls\.items\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.stage\_2\_iocs\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.stage\_2\_iocs\.properties\.md5\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.stage\_2\_iocs\.properties\.size\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.stage\_2\_iocs\.properties\.files\.type | string |  `file name` 
action\_result\.data\.\*\.attributes\.body\.properties\.stage\_2\_iocs\.properties\.c2\_ips\.type | string |  `ip` 
action\_result\.data\.\*\.attributes\.body\.properties\.stage\_2\_iocs\.properties\.c2\_urls\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.stage\_2\_iocs\.properties\.payload\_ips\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.stage\_2\_iocs\.properties\.payload\_ips\.items\.type | string |  `ip` 
action\_result\.data\.\*\.attributes\.body\.properties\.stage\_2\_iocs\.properties\.payload\_urls\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.stage\_2\_iocs\.properties\.payload\_urls\.items\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.received\_time\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.reported\_time\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.vision\_results\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.vision\_results\.properties\.results\_id | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.vision\_results\.properties\.query\_created\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.vision\_results\.properties\.messages\_found | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.vision\_results\.properties\.messages\_removed | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.escalation\_type\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.malware\_families\.type | string | 
action\_result\.data\.\*\.attributes\.tags | string |  `cofensetriage tag` 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary\.total\_comments\_retrieved | numeric | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'get comment'
Retrieve a comment from the Cofense Triage Platform for the provided comment ID

Type: **investigate**  
Read only: **True**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**comment\_id** |  required  | ID of the comment | numeric |  `cofensetriage comment id` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.comment\_id | numeric |  `cofensetriage comment id` 
action\_result\.data\.\*\.id | string |  `cofensetriage comment id` 
action\_result\.data\.\*\.type | string | 
action\_result\.data\.\*\.links\.self | string |  `url` 
action\_result\.data\.\*\.attributes\.body | string | 
action\_result\.data\.\*\.attributes\.created\_at | string |  `date` 
action\_result\.data\.\*\.attributes\.updated\_at | string |  `date` 
action\_result\.data\.\*\.attributes\.body\_format | string |  `cofensetriage comment body format` 
action\_result\.data\.\*\.relationships\.owner\.data\.id | string | 
action\_result\.data\.\*\.relationships\.owner\.data\.type | string | 
action\_result\.data\.\*\.relationships\.owner\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.owner\.links\.related | string |  `url` 
action\_result\.data\.\*\.relationships\.commentable\.data\.id | string | 
action\_result\.data\.\*\.relationships\.commentable\.data\.type | string | 
action\_result\.data\.\*\.relationships\.commentable\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.commentable\.links\.related | string |  `url` 
action\_result\.data\.\*\.attributes\.body\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.from\.type | string |  `email` 
action\_result\.data\.\*\.attributes\.body\.properties\.notes\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.brands\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.brands\.items\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.srctag\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.sent\_to\.type | string |  `email` 
action\_result\.data\.\*\.attributes\.body\.properties\.subject\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.summary\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.reply\_to\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.report\_id\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.message\_id\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.phenotypes\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.report\_url\.type | string |  `url` 
action\_result\.data\.\*\.attributes\.body\.properties\.reported\_by\.type | string |  `email` 
action\_result\.data\.\*\.attributes\.body\.properties\.stage\_1\_iocs\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.stage\_1\_iocs\.properties\.files\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.stage\_1\_iocs\.properties\.infection\_ips\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.stage\_1\_iocs\.properties\.infection\_ips\.items\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.stage\_1\_iocs\.properties\.infection\_urls\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.stage\_1\_iocs\.properties\.infection\_urls\.items\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.stage\_2\_iocs\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.stage\_2\_iocs\.properties\.md5\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.stage\_2\_iocs\.properties\.size\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.stage\_2\_iocs\.properties\.files\.type | string |  `file name` 
action\_result\.data\.\*\.attributes\.body\.properties\.stage\_2\_iocs\.properties\.c2\_ips\.type | string |  `ip` 
action\_result\.data\.\*\.attributes\.body\.properties\.stage\_2\_iocs\.properties\.c2\_urls\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.stage\_2\_iocs\.properties\.payload\_ips\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.stage\_2\_iocs\.properties\.payload\_ips\.items\.type | string |  `ip` 
action\_result\.data\.\*\.attributes\.body\.properties\.stage\_2\_iocs\.properties\.payload\_urls\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.stage\_2\_iocs\.properties\.payload\_urls\.items\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.received\_time\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.reported\_time\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.vision\_results\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.vision\_results\.properties\.results\_id | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.vision\_results\.properties\.query\_created\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.vision\_results\.properties\.messages\_found | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.vision\_results\.properties\.messages\_removed | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.escalation\_type\.type | string | 
action\_result\.data\.\*\.attributes\.body\.properties\.malware\_families\.type | string | 
action\_result\.data\.\*\.attributes\.tags | string |  `cofensetriage tag` 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'get rules'
Retrieve rules from the Cofense Triage Platform filtered based on the provided parameters

Type: **investigate**  
Read only: **True**

If no value is provided in any parameter, then all the records will be retrieved\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**name** |  optional  | Allows filtering the rules based on the name | string |  `cofensetriage rule name` 
**description** |  optional  | Allows filtering the rules based on the description | string |  `cofensetriage rule description` 
**priority** |  optional  | Allows filtering the rules based on the priority | numeric |  `cofensetriage priority` 
**tags** |  optional  | Allows filtering the rules based on the list of comma\-separated tags\. If the tag value contains a comma, enclose it in double\-quotes \(Example\: tag1,"test,tag",tag2\) | string |  `cofensetriage tag` 
**scope** |  optional  | Allows filtering the rules based on the scope | string |  `cofensetriage rule scope` 
**author\_name** |  optional  | Allows filtering the rules based on the author name | string |  `cofensetriage rule author name` 
**rule\_context** |  optional  | Allows filtering the rules based on the context | string |  `cofensetriage rule context` 
**active** |  optional  | Allows filtering the rules based on the status | boolean | 
**reports\_count** |  optional  | Allows filtering the rules based on the number of reports the rule matched | numeric |  `cofensetriage rule reports count` 
**reports\_count\_operator** |  optional  | Operator to work with the reports count parameter | string | 
**start\_date** |  optional  | Allows filtering the rules updated on or after the provided date | string |  `date` 
**end\_date** |  optional  | Allows filtering the rules updated before the provided date | string |  `date` 
**sort** |  optional  | Allows sorting the rules based on the 'updated\_at' date of the rule | string | 
**max\_results** |  optional  | Maximum number of results to return | numeric | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.name | string |  `cofensetriage rule name` 
action\_result\.parameter\.description | string |  `cofensetriage rule description` 
action\_result\.parameter\.priority | numeric |  `cofensetriage priority` 
action\_result\.parameter\.tags | string |  `cofensetriage tag` 
action\_result\.parameter\.scope | string |  `cofensetriage rule scope` 
action\_result\.parameter\.author\_name | string |  `cofensetriage rule author name` 
action\_result\.parameter\.rule\_context | string |  `cofensetriage rule context` 
action\_result\.parameter\.active | boolean | 
action\_result\.parameter\.reports\_count | numeric |  `cofensetriage rule reports count` 
action\_result\.parameter\.reports\_count\_operator | string | 
action\_result\.parameter\.start\_date | string |  `date` 
action\_result\.parameter\.end\_date | string |  `date` 
action\_result\.parameter\.sort | string | 
action\_result\.parameter\.max\_results | numeric | 
action\_result\.data\.\*\.id | string |  `cofensetriage rule id` 
action\_result\.data\.\*\.type | string | 
action\_result\.data\.\*\.links\.self | string |  `url` 
action\_result\.data\.\*\.attributes\.name | string |  `cofensetriage rule name` 
action\_result\.data\.\*\.attributes\.scope | string |  `cofensetriage rule scope` 
action\_result\.data\.\*\.attributes\.active | boolean | 
action\_result\.data\.\*\.attributes\.content | string | 
action\_result\.data\.\*\.attributes\.priority | numeric |  `cofensetriage priority` 
action\_result\.data\.\*\.attributes\.created\_at | string |  `date` 
action\_result\.data\.\*\.attributes\.updated\_at | string |  `date` 
action\_result\.data\.\*\.attributes\.author\_name | string |  `cofensetriage rule author name` 
action\_result\.data\.\*\.attributes\.description | string |  `cofensetriage rule description` 
action\_result\.data\.\*\.attributes\.imported\_at | string | 
action\_result\.data\.\*\.attributes\.rule\_context | string |  `cofensetriage rule context` 
action\_result\.data\.\*\.attributes\.time\_to\_live | string | 
action\_result\.data\.\*\.attributes\.reports\_count | numeric |  `cofensetriage rule reports count` 
action\_result\.data\.\*\.attributes\.share\_with\_cofense | boolean | 
action\_result\.data\.\*\.relationships\.owner\.data\.id | string | 
action\_result\.data\.\*\.relationships\.owner\.data\.type | string | 
action\_result\.data\.\*\.relationships\.owner\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.owner\.links\.related | string |  `url` 
action\_result\.data\.\*\.relationships\.reports\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.reports\.links\.related | string |  `url` 
action\_result\.data\.\*\.relationships\.clusters\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.clusters\.links\.related | string |  `url` 
action\_result\.data\.\*\.relationships\.report\_context\.data | string | 
action\_result\.data\.\*\.relationships\.report\_context\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.report\_context\.links\.related | string |  `url` 
action\_result\.data\.\*\.relationships\.cluster\_context\.data | string | 
action\_result\.data\.\*\.relationships\.cluster\_context\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.cluster\_context\.links\.related | string |  `url` 
action\_result\.data\.\*\.attributes\.tags | string |  `cofensetriage tag` 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary\.total\_rules\_retrieved | numeric | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'get rule'
Retrieve a rule from the Cofense Triage Platform for the provided rule ID

Type: **investigate**  
Read only: **True**

If the 'ingest\_subfields' parameter is true, the report and the subfields together will get ingested into the container\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**rule\_id** |  required  | ID of the rule | numeric |  `cofensetriage rule id` 
**ingest\_report** |  optional  | Allows ingestion of the reports related to the rule into the container | boolean | 
**ingest\_subfields** |  optional  | Allows ingestion of fields relating to the report into the container | boolean | 
**label** |  optional  | Allows ingestion of data into the container\(s\) with the provided label\. The label must be valid or the action will fail\. Required if 'ingest\_report' or 'ingest\_subfields' is set | string | 
**tenant** |  optional  | Allows creation of container\(s\) for the provided tenant ID or tenant name\. The tenant must be valid or the action will fail\. Required if 'ingest\_report' or 'ingest\_subfields' is set | string | 
**cef\_mapping** |  optional  | JSON dictionary represented as a serialized JSON string\. Each key in the dictionary is a potential key name in an artifact that is to be renamed to the value | string | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.rule\_id | numeric |  `cofensetriage rule id` 
action\_result\.parameter\.ingest\_report | boolean | 
action\_result\.parameter\.ingest\_subfields | boolean | 
action\_result\.parameter\.label | string | 
action\_result\.parameter\.tenant | string | 
action\_result\.parameter\.cef\_mapping | string | 
action\_result\.data\.\*\.id | string |  `cofensetriage rule id` 
action\_result\.data\.\*\.type | string | 
action\_result\.data\.\*\.links\.self | string |  `url` 
action\_result\.data\.\*\.reports\.\*\.id | string |  `cofensetriage report id` 
action\_result\.data\.\*\.reports\.\*\.meta\.risk\_score\_summary\.vip | numeric | 
action\_result\.data\.\*\.reports\.\*\.meta\.risk\_score\_summary\.rules | numeric | 
action\_result\.data\.\*\.reports\.\*\.meta\.risk\_score\_summary\.reporter | numeric | 
action\_result\.data\.\*\.reports\.\*\.meta\.risk\_score\_summary\.integrations | numeric | 
action\_result\.data\.\*\.reports\.\*\.type | string | 
action\_result\.data\.\*\.reports\.\*\.links\.self | string |  `url` 
action\_result\.data\.\*\.reports\.\*\.attributes\.md5 | string |  `md5` 
action\_result\.data\.\*\.reports\.\*\.attributes\.sha256 | string |  `sha256` 
action\_result\.data\.\*\.reports\.\*\.attributes\.subject | string |  `cofensetriage report subject` 
action\_result\.data\.\*\.reports\.\*\.attributes\.location | string |  `cofensetriage report location` 
action\_result\.data\.\*\.reports\.\*\.attributes\.html\_body | string | 
action\_result\.data\.\*\.reports\.\*\.attributes\.text\_body | string | 
action\_result\.data\.\*\.reports\.\*\.attributes\.created\_at | string |  `date` 
action\_result\.data\.\*\.reports\.\*\.attributes\.risk\_score | numeric |  `cofensetriage risk score` 
action\_result\.data\.\*\.reports\.\*\.attributes\.updated\_at | string |  `date` 
action\_result\.data\.\*\.reports\.\*\.attributes\.raw\_headers | string | 
action\_result\.data\.\*\.reports\.\*\.attributes\.received\_at | string |  `date` 
action\_result\.data\.\*\.reports\.\*\.attributes\.reported\_at | string |  `date` 
action\_result\.data\.\*\.reports\.\*\.attributes\.from\_address | string |  `email` 
action\_result\.data\.\*\.reports\.\*\.attributes\.processed\_at | string |  `date` 
action\_result\.data\.\*\.reports\.\*\.attributes\.match\_priority | numeric |  `cofensetriage priority` 
action\_result\.data\.\*\.reports\.\*\.container\_id | numeric |  `container id` 
action\_result\.data\.\*\.reports\.\*\.relationships\.urls\.links\.self | string |  `url` 
action\_result\.data\.\*\.reports\.\*\.relationships\.urls\.links\.related | string |  `url` 
action\_result\.data\.\*\.reports\.\*\.relationships\.rules\.links\.self | string |  `url` 
action\_result\.data\.\*\.reports\.\*\.relationships\.rules\.links\.related | string |  `url` 
action\_result\.data\.\*\.reports\.\*\.relationships\.cluster\.data\.id | string | 
action\_result\.data\.\*\.reports\.\*\.relationships\.cluster\.data\.type | string | 
action\_result\.data\.\*\.reports\.\*\.relationships\.cluster\.links\.self | string |  `url` 
action\_result\.data\.\*\.reports\.\*\.relationships\.cluster\.links\.related | string |  `url` 
action\_result\.data\.\*\.reports\.\*\.relationships\.domains\.links\.self | string |  `url` 
action\_result\.data\.\*\.reports\.\*\.relationships\.domains\.links\.related | string |  `url` 
action\_result\.data\.\*\.reports\.\*\.relationships\.headers\.links\.self | string |  `url` 
action\_result\.data\.\*\.reports\.\*\.relationships\.headers\.links\.related | string |  `url` 
action\_result\.data\.\*\.reports\.\*\.relationships\.assignee\.data | string | 
action\_result\.data\.\*\.reports\.\*\.relationships\.assignee\.links\.self | string |  `url` 
action\_result\.data\.\*\.reports\.\*\.relationships\.assignee\.links\.related | string |  `url` 
action\_result\.data\.\*\.reports\.\*\.relationships\.category\.data | string | 
action\_result\.data\.\*\.reports\.\*\.relationships\.category\.links\.self | string |  `url` 
action\_result\.data\.\*\.reports\.\*\.relationships\.category\.links\.related | string |  `url` 
action\_result\.data\.\*\.reports\.\*\.relationships\.comments\.links\.self | string |  `url` 
action\_result\.data\.\*\.reports\.\*\.relationships\.comments\.links\.related | string |  `url` 
action\_result\.data\.\*\.reports\.\*\.relationships\.reporter\.data\.id | string |  `cofensetriage reporter id` 
action\_result\.data\.\*\.reports\.\*\.relationships\.reporter\.data\.type | string | 
action\_result\.data\.\*\.reports\.\*\.relationships\.reporter\.links\.self | string |  `url` 
action\_result\.data\.\*\.reports\.\*\.relationships\.reporter\.links\.related | string |  `url` 
action\_result\.data\.\*\.reports\.\*\.relationships\.hostnames\.links\.self | string |  `url` 
action\_result\.data\.\*\.reports\.\*\.relationships\.hostnames\.links\.related | string |  `url` 
action\_result\.data\.\*\.reports\.\*\.relationships\.attachments\.links\.self | string |  `url` 
action\_result\.data\.\*\.reports\.\*\.relationships\.attachments\.links\.related | string |  `url` 
action\_result\.data\.\*\.reports\.\*\.relationships\.threat\_indicators\.links\.self | string |  `url` 
action\_result\.data\.\*\.reports\.\*\.relationships\.threat\_indicators\.links\.related | string |  `url` 
action\_result\.data\.\*\.reports\.\*\.relationships\.attachment\_payloads\.links\.self | string |  `url` 
action\_result\.data\.\*\.reports\.\*\.relationships\.attachment\_payloads\.links\.related | string |  `url` 
action\_result\.data\.\*\.attributes\.name | string |  `cofensetriage rule name` 
action\_result\.data\.\*\.attributes\.tags | string |  `cofensetriage tag` 
action\_result\.data\.\*\.attributes\.scope | string |  `cofensetriage rule scope` 
action\_result\.data\.\*\.attributes\.active | boolean | 
action\_result\.data\.\*\.attributes\.content | string | 
action\_result\.data\.\*\.attributes\.priority | numeric |  `cofensetriage priority` 
action\_result\.data\.\*\.attributes\.created\_at | string |  `date` 
action\_result\.data\.\*\.attributes\.updated\_at | string |  `date` 
action\_result\.data\.\*\.attributes\.author\_name | string |  `cofensetriage rule author name` 
action\_result\.data\.\*\.attributes\.description | string |  `cofensetriage rule description` 
action\_result\.data\.\*\.attributes\.imported\_at | string | 
action\_result\.data\.\*\.attributes\.rule\_context | string |  `cofensetriage rule context` 
action\_result\.data\.\*\.attributes\.time\_to\_live | string | 
action\_result\.data\.\*\.attributes\.reports\_count | numeric |  `cofensetriage rule reports count` 
action\_result\.data\.\*\.attributes\.share\_with\_cofense | boolean | 
action\_result\.data\.\*\.relationships\.owner\.data\.id | string | 
action\_result\.data\.\*\.relationships\.owner\.data\.type | string | 
action\_result\.data\.\*\.relationships\.owner\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.owner\.links\.related | string |  `url` 
action\_result\.data\.\*\.relationships\.reports\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.reports\.links\.related | string |  `url` 
action\_result\.data\.\*\.relationships\.clusters\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.clusters\.links\.related | string |  `url` 
action\_result\.data\.\*\.relationships\.report\_context\.data | string | 
action\_result\.data\.\*\.relationships\.report\_context\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.report\_context\.links\.related | string |  `url` 
action\_result\.data\.\*\.relationships\.cluster\_context\.data | string | 
action\_result\.data\.\*\.relationships\.cluster\_context\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.cluster\_context\.links\.related | string |  `url` 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'get integration submissions'
Retrieve integration submissions from the Cofense Triage Platform filtered based on the provided parameters

Type: **investigate**  
Read only: **True**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**type** |  required  | The type of integration submission | string | 
**value** |  required  | The value of integration submission | string |  `hash`  `md5`  `sha256`  `url` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.type | string | 
action\_result\.parameter\.value | string |  `hash`  `md5`  `sha256`  `url` 
action\_result\.data\.\*\.id | string | 
action\_result\.data\.\*\.type | string | 
action\_result\.data\.\*\.links\.self | string |  `url` 
action\_result\.data\.\*\.attributes\.kind | string | 
action\_result\.data\.\*\.attributes\.result | string | 
action\_result\.data\.\*\.attributes\.status | string | 
action\_result\.data\.\*\.attributes\.risk\_score | numeric |  `cofensetriage risk score` 
action\_result\.data\.\*\.attributes\.created\_at | string |  `date` 
action\_result\.data\.\*\.attributes\.updated\_at | string |  `date` 
action\_result\.data\.\*\.relationships\.target\.data\.id | string | 
action\_result\.data\.\*\.relationships\.target\.data\.type | string | 
action\_result\.data\.\*\.relationships\.target\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.target\.links\.related | string |  `url` 
action\_result\.data\.\*\.relationships\.integration\.data\.id | string | 
action\_result\.data\.\*\.relationships\.integration\.data\.type | string | 
action\_result\.data\.\*\.relationships\.integration\.links\.self | string |  `url` 
action\_result\.data\.\*\.relationships\.integration\.links\.related | string |  `url` 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary\.total\_integration\_submissions\_retrieved | numeric | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'on poll'
Action handler for the on poll ingest functionality

Type: **ingest**  
Read only: **True**

This action ingests reports or threat indicators from Cofense Triage as per the selected ingestion type\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**container\_count** |  optional  | Maximum number of containers to ingest | numeric | 
**start\_time** |  optional  | Parameter ignored in this app | numeric | 
**end\_time** |  optional  | Parameter ignored in this app | numeric | 
**artifact\_count** |  optional  | Parameter ignored in this app | numeric | 

#### Action Output
No Output