# 🤖 AI Twitter Autopilot

> Automated Twitter/X content creation powered by OpenAI GPT-4 and n8n workflow automation


## 📋 Overview

AI Twitter Autopilot is an intelligent n8n workflow that automatically generates and posts engaging Twitter/X content using OpenAI's GPT-4. Simply maintain your content ideas in a Google Sheet, and let AI handle the rest – from content generation to posting and tracking.

## ✨ Features

- 📊 **Google Sheets Integration** - Manage content ideas in a centralized spreadsheet
- 🤖 **AI-Powered Content Generation** - GPT-4 creates engaging, platform-optimized posts
- 🔀 **Smart Platform Routing** - Conditional logic for multi-platform support
- 🐦 **Direct Twitter/X Posting** - Automated publishing with OAuth authentication
- 📝 **Post Tracking** - Updates spreadsheet with posting status and timestamps
- ⚡ **Fully Automated** - Set it and forget it workflow execution

## 🛠️ Prerequisites

Before you begin, ensure you have:

- [n8n](https://n8n.io) installed (self-hosted or cloud)
- OpenAI API key ([Get one here](https://platform.openai.com/api-keys))
- Twitter/X Developer Account with API access ([Apply here](https://developer.twitter.com))
- Google Cloud Project with Sheets API enabled
- Google Service Account credentials

## 📦 Installation

### 1. Download the Workflow

Download the `ai-twitter-autopilot.json` file from this repository.

### 2. Import to n8n

1. Open your n8n instance
2. Go to **Workflows** → Click **"Import from File"**
3. Select the downloaded `Create_Twitter_X_Post.json`
4. Click **"Import"**

### 3. Configure Credentials

#### OpenAI API
1. Go to **Credentials** → **Create New**
2. Select **OpenAI API**
3. Enter your API key
4. Name it: `OpenAI GPT-4`

#### Twitter/X OAuth
1. Go to **Credentials** → **Create New**
2. Select **Twitter OAuth1 API**
3. Enter your:
   - API Key
   - API Secret
   - Access Token
   - Access Token Secret
4. Name it: `Twitter API`

#### Google Sheets
1. Go to **Credentials** → **Create New**
2. Select **Google Sheets API**
3. Upload your service account JSON
4. Grant access to your spreadsheet

### 4. Setup Google Sheet

Create a Google Sheet with this structure:

| Column A | Column B | Column C |
|----------|----------|----------|
| **Idea** | **Platform** | **Status** |
| Launch new feature | Twitter | Pending |
| Product tips | Twitter | Pending |

**Share the sheet** with your service account email (found in your JSON credentials).

### 5. Update Workflow Configuration

1. In n8n, click the **"Get Content Ideas"** node
2. Replace `YOUR_GOOGLE_SHEET_ID` with your Sheet ID (from URL)
3. Update range if needed (default: `Sheet1!A:C`)
4. Click the **"Update Google Sheet"** node
5. Replace Sheet ID there as well

## 🚀 Usage

### Manual Execution
1. Add content ideas to your Google Sheet
2. Open the workflow in n8n
3. Click **"Execute Workflow"**
4. Monitor execution in real-time

### Scheduled Execution (Optional)
1. Add a **Schedule Trigger** node before "Get Content Ideas"
2. Configure frequency (e.g., daily at 10 AM)
3. Activate the workflow
4. Posts will be created automatically

## 📊 Workflow Architecture

```
Google Sheets → OpenAI GPT-4 → Platform Check → Twitter/X API → Update Sheet
     ↓              ↓                ↓              ↓              ↓
  Read Ideas   Generate Post   Route Logic    Publish Post   Track Status
```

## 🔧 Customization

### Change AI Prompt
Edit the **"Generate Post with OpenAI"** node prompt:
```
Create a social media post for {{$node["Get Content Ideas"].json["Platform"]}} 
based on this idea: {{$node["Get Content Ideas"].json["Idea"]}}. 
Keep it engaging and concise.
```

### Add More Platforms
Duplicate the **"Check Platform"** condition and add nodes for LinkedIn, Facebook, etc.

## ⚠️ Troubleshooting

| Issue | Solution |
|-------|----------|
| "Sheet not found" | Check Sheet ID and sharing permissions |
| "OpenAI API error" | Verify API key and account credits |
| "Twitter auth failed" | Regenerate OAuth tokens |
| Workflow won't save | Check all credential fields are filled |


## 🙏 Credits

Built with [n8n](https://n8n.io), [OpenAI](https://openai.com), and [Twitter API](https://developer.twitter.com)

---

⭐ **Star this repo** if you find it useful!
