# Google Sheets Integration Setup Guide

## Overview

BharatBiz.AI can connect to Google Sheets to fetch real sales and inventory data. This guide shows you how to set it up.

---

## Step 1: Create Google Cloud Project

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create a new project (or select existing)
3. Note your project name

---

## Step 2: Enable Google Sheets API

1. In Google Cloud Console, go to **APIs & Services** > **Library**
2. Search for "Google Sheets API"
3. Click **Enable**

---

## Step 3: Create Service Account

1. Go to **APIs & Services** > **Credentials**
2. Click **Create Credentials** > **Service Account**
3. Fill in:
   - **Service account name**: `bharatbiz-sheets`
   - **Service account ID**: (auto-generated)
   - Click **Create and Continue**
4. Skip role assignment (click **Continue**)
5. Click **Done**

---

## Step 4: Create Service Account Key

1. Click on the service account you just created
2. Go to **Keys** tab
3. Click **Add Key** > **Create new key**
4. Choose **JSON** format
5. Download the JSON file
6. **Save it securely** - this is your credentials file

---

## Step 5: Create Google Sheet

1. Create a new Google Sheet
2. Name it: `BharatBiz Sales Data`
3. Create two worksheets:

### Worksheet 1: "Sales"
Format:
```
| Date       | Sales | Orders |
|------------|-------|--------|
| 2024-01-01 | 3500  | 25     |
| 2024-01-02 | 4200  | 30     |
| 2024-01-03 | 3800  | 28     |
```

### Worksheet 2: "Inventory"
Format:
```
| Product   | Stock | Low Stock Threshold |
|-----------|-------|---------------------|
| Product A | 45    | 20                   |
| Product B | 15    | 20                   |
| Product C | 8     | 10                   |
```

---

## Step 6: Share Sheet with Service Account

1. In your Google Sheet, click **Share** button
2. Get the service account email from the JSON file (look for `"client_email"`)
3. Paste the email address
4. Give it **Viewer** access (read-only)
5. Click **Send**

---

## Step 7: Configure Backend

1. Copy the downloaded JSON file to `backend/` directory
2. Rename it to `google-credentials.json` (or any name you prefer)
3. Add to `.env` file:

```env
GOOGLE_SHEETS_CREDENTIALS_PATH=backend/google-credentials.json
GOOGLE_SHEETS_URL=https://docs.google.com/spreadsheets/d/YOUR_SHEET_ID/edit
```

**To get Sheet ID:**
- Open your Google Sheet
- Look at the URL: `https://docs.google.com/spreadsheets/d/SHEET_ID_HERE/edit`
- Copy the `SHEET_ID_HERE` part

---

## Step 8: Install Dependencies

```bash
cd backend
pip install gspread google-auth
```

Or update requirements.txt (already done):
```bash
pip install -r requirements.txt
```

---

## Step 9: Test Connection

1. Start backend: `python backend/app.py`
2. Check console logs for: `[INFO] Google Sheets client initialized successfully`
3. Visit dashboard: `http://localhost:3000/dashboard`
4. You should see real data from your sheet!

---

## Troubleshooting

### Error: "Permission denied"
- Make sure you shared the sheet with the service account email
- Check that the email in JSON matches the one you shared with

### Error: "File not found"
- Check the path in `.env` file
- Make sure JSON file exists at that path

### Error: "API not enabled"
- Go back to Google Cloud Console
- Enable Google Sheets API
- Wait a few minutes for propagation

### Still using mock data?
- Check backend logs for: `[INFO] Using Google Sheets data`
- If you see `[INFO] Using mock data`, check your configuration

---

## Security Notes

⚠️ **Important:**
- Never commit `google-credentials.json` to Git
- Add it to `.gitignore`:
  ```
  backend/google-credentials.json
  backend/*credentials*.json
  ```
- Keep your credentials file secure
- Use environment variables for paths

---

## Optional: Multiple Sheets

You can use different sheets for different businesses:

```env
GOOGLE_SHEETS_URL=https://docs.google.com/spreadsheets/d/SHEET_ID_1/edit
```

Or modify `sheets_integration.py` to support multiple sheets.

---

## Data Format Requirements

### Sales Sheet
- **Date column**: Must be in `YYYY-MM-DD` format
- **Sales column**: Numeric values (amounts)
- **Orders column**: Integer values (count)

### Inventory Sheet
- **Product column**: Product names
- **Stock column**: Current stock count (integer)
- **Low Stock Threshold column**: Minimum stock level (integer)

---

## Example Sheet Templates

### Sales Template
```
Date       | Sales | Orders
2024-01-15 | 3500  | 25
2024-01-16 | 4200  | 30
2024-01-17 | 3800  | 28
2024-01-18 | 4500  | 32
2024-01-19 | 5200  | 38
2024-01-20 | 6800  | 48
2024-01-21 | 5500  | 40
```

### Inventory Template
```
Product   | Stock | Low Stock Threshold
Product A | 45    | 20
Product B | 15    | 20
Product C | 8     | 10
Product D | 30    | 15
```

---

## Next Steps

Once connected:
1. Update your sheet regularly with sales data
2. Dashboard will automatically show real-time insights
3. Forecasting will improve with more historical data
4. Recommendations will be based on actual trends

---

**Need Help?** Check backend logs for detailed error messages!

