# StudyMate Setup Guide

## Prerequisites
- n8n account or local n8n installation
- Google APIs credentials (Sheets + Gmail)
- Unsplash API key
- Google Gemini API key
- Google Form (see below)
- Google Sheet linked to the Form (see below)

## Step 1 – Create Google Form
Create a form with these elements:

| Field Name | Element Type | Placeholder / Options | Required |
|------------|-------------|--------------------|---------|
| Full Name  | Text | e.g: Sara, Yasir | Yes |
| Email | Email | e.g: john@gmail.com | Yes |
| Interest? (Pick as Many as you want) | Dropdown / Multiple Choice | AI<br>Quantum Computing<br>Cyber Security<br>Data Science and Analytics<br>Game Development<br>Software Development<br>Web Development | Yes |
| Email Tones? (What kind of newsletter you love to read?) | Dropdown | Casual<br>Sarcastic<br>Professional / Formal<br>Story Telling Format<br>Neutral | Yes |

> Make sure your form is **linked to a Google Sheet** to collect responses.

## Step 2 – Create Google Sheet
Your Google Sheet should have the following **column names**:

| Column Name | Value Mapping from Form |
|-------------|------------------------|
| Name | `{{ $json["Full Name"] }}` |
| Email | `{{ $json.Email }}` |
| Interest | `{{ $json["Interest? (Pick as Many as you want)"] }}` |
| Tone | `{{ $json["Email Tones? (What kind of newsletter you love to read?)"] }}` |

> This Sheet is where n8n will read subscriber data for generating personalized newsletters.

## Step 3 – Import Workflow
1. Download `LeadConnect_Workflow.json` from repo.
2. In n8n, click **Import** → select the JSON file.
3. Workflow nodes will appear fully connected.

## Step 4 – Set Credentials
- **Google Sheets**: OAuth2 credentials for reading/writing subscriber data.
- **Gmail**: OAuth2 credentials for sending emails.
- **Unsplash**: API key for fetching images.
- **Google Gemini**: API key for AI content generation.

## Step 5 – Configure Workflow
- Schedule Trigger: Set interval for automated newsletter sending.
- Form Trigger: Use the public Google Form link created above.
- Update API keys in HTTP Request nodes (Unsplash, GNews, Gemini).

## Step 6 – Run Workflow
1. Activate the workflow.
2. Test form submission → subscriber appears in Google Sheet.
3. Verify AI-generated newsletter output in Gmail.

## Optional – Customizations
- Add more interests or tones in `Categorize into Interests` code node.
- Adjust newsletter template (colors, layout) in `Newsletter Generator` node.
- Extend to other APIs for content sourcing.

## Notes
- All AI-generated content is handled inside n8n nodes – no external scripts required.
- Inline CSS ensures newsletters display properly across Gmail/Outlook.
