# 📧 Automated Email Reports  

## 🚀 Overview  
This Google Apps Script automates email reports by extracting data from Google Sheets, formatting the content, and sending it via email on a scheduled basis. This helps businesses automate daily, weekly, or monthly reports without manual effort.  

## 🔹 Features  
✅ Extracts data from Google Sheets  
✅ Sends formatted email reports  
✅ Supports automated scheduling with triggers  
✅ Easy customization for different data sources  

## 📌 How It Works  
1. The script fetches data from a Google Sheet.  
2. Formats the extracted data into a readable email.  
3. Sends the email automatically to a predefined recipient.  
4. Can be scheduled using Google Apps Script triggers (e.g., daily, weekly).  

## 🛠️ Setup Instructions  
1. Open Google Sheets and go to **Extensions → Apps Script**.  
2. Delete any existing code and paste the contents of `sendEmail.gs`.  
3. Modify the `recipient@example.com` email in the script.  
4. Rename your Google Sheet to match the script’s expected sheet name (default: "Sales Report").  
5. Go to **Triggers** (clock icon) and set a time-based trigger (e.g., run daily).  

## 📩 Example Email Output  
![Email Report](https://i.imgur.com/5cKuhrp.png)



## 📜 Script Code (`sendEmail.gs`)  

```javascript
function sendAutomatedEmail() {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName("Sales Report");
  var data = sheet.getDataRange().getValues();
  
  var totalSales = data[1][1]; // Fetching total sales from row 2, column 2
  var bestSeller = data[2][1]; // Fetching best seller info
  
  var subject = "📊 Daily Sales Report";
  
  var htmlBody = `
    <div style="font-family: Arial, sans-serif; max-width: 500px; background: #ffffff; padding: 20px; 
                border-radius: 8px; box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);">
      <h2 style="color: #333366; border-bottom: 2px solid #333366; padding-bottom: 5px;">📊 Daily Sales Report</h2>
      <p>Hello Team,</p>
      <p>Here is your sales report for today:</p>
      <div style="background: #eeeeee; padding: 10px; border-radius: 5px; margin-top: 10px;">
        <p><strong>Total Sales:</strong> <span style="color: green;">$${totalSales}</span></p>
        <p><strong>Best Seller:</strong> ${bestSeller}</p>
      </div>
      <p>Regards,<br>Automated System</p>
      <div style="margin-top: 20px; font-size: 12px; color: #777777;">
        <p>This is an automated email. Please do not reply.</p>
      </div>
    </div>
  `;
  
  MailApp.sendEmail({
    to: "recipient@example.com",
    subject: subject,
    htmlBody: htmlBody
  });
}
