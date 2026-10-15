# AI Lead Generation & Qualification Automation

An n8n workflow that receives lead information through a webhook,
validates email addresses, checks Google Sheets for duplicate leads,
uses an AI model to qualify new leads, and stores the results in a
Google Sheets CRM.

## Project Overview

The goal of this project is to automate repetitive lead intake and
qualification tasks so that incoming leads can be organized in one place
and processed consistently.

## Workflow

1.  **Webhook intake** --- receives lead data from an incoming request.
2.  **Email validation** --- checks whether the submitted email follows
    a valid email format.
3.  **Duplicate detection** --- searches the Google Sheets CRM for an
    existing record with the same email.
4.  **AI lead qualification** --- sends new leads to an LLM chain for
    qualification.
5.  **CRM storage** --- adds the processed lead and qualification
    details to the `Leads` worksheet.
6.  **Error-handling path** --- routes LLM failures to a separate Google
    Sheets worksheet named `Failed Leads`.

## Main Features

-   Webhook-based lead intake
-   Email format validation
-   Duplicate lead detection using email
-   AI-assisted lead qualification
-   Google Sheets CRM integration
-   Separate worksheet for failed AI-processing runs
-   Timestamp field for failure records

## Tools and Technologies

-   **n8n** --- workflow automation
-   **Google Sheets** --- lead CRM and failure log
-   **Gemini / Google AI model** --- AI processing through the
    configured chat model
-   **Webhook** --- receives incoming lead data

## Google Sheets Structure

The workflow uses a Google Sheets document with these worksheets:

### `Leads`

Stores new leads and the qualification fields configured in the
workflow.

### `Failed Leads`

Designed to record failed processing attempts. The current columns are:

-   `Email`
-   `Status`
-   `Error`
-   `Timestamp`

## Example Input

Send a JSON request to the workflow's webhook using the field names
expected by your workflow. A minimal example is:

``` json
{
  "name": "Ali",
  "email": "ali@example.com",
  "company": "Example Company",
  "message": "I am interested in your service."
}
```

> Adjust the example fields to match the exact input schema configured
> in your webhook and AI prompt.

## Setup

To run this workflow in another n8n instance:

1.  Export the workflow from your n8n workspace as a workflow JSON file.
2.  Import the JSON file into n8n.
3.  Connect your Google account and select the appropriate Google Sheets
    document and worksheets.
4.  Configure the Gemini / Google AI credentials and select an available
    model.
5.  Confirm the Google Sheets column mappings match your spreadsheet.
6.  Activate or execute the workflow as appropriate for your use case.
7.  Send a test request to the webhook and check the resulting row in
    Google Sheets.

**Important:** Credentials, API keys, webhook secrets, and private lead
data should not be included in a public repository. Review the exported
workflow JSON before publishing it and remove any sensitive values.

## Testing Checklist

-   [ ] Submit a new lead with a valid email and confirm it is added to
    `Leads`.
-   [ ] Submit the same email again and confirm the duplicate is not
    added.
-   [ ] Submit an invalid email and confirm the validation branch
    behaves as expected.
-   [ ] Trigger a controlled LLM failure and verify the error-handling
    branch and `Failed Leads` row.
-   [ ] Confirm no credentials or private lead data are present in
    public files.

## Project Status

The main lead-processing workflow has been built and tested. The
error-handling branch is configured; verify that a failed run creates
the expected row in `Failed Leads` before describing that logging path
as fully tested.

## Future Improvements

-   Add a dedicated response for invalid email submissions.
-   Improve handling of missing or incomplete lead fields.
-   Add notifications for qualified leads or failed executions.
-   Add a dashboard for lead status and qualification results.

## Author

**Umair Ali**\
GitHub: [@umairdevh7](https://github.com/umairdevh7)
