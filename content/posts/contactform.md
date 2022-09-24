---
title: "Make your contact form working without using a server"
date: 2022-09-24T18:10:48+05:30
draft: true
---

## The Problem

I was trying to make a contact form for my website. I was using [Formspree](https://formspree.io/) for that. But I as a fellow developer I love to learn new things. So I decided to make my own contact form without using any server. I hope this tutorial will help you to make your own contact form without using any server.

## Introduction

In this tutorial, we will learn how to make a contact form that will work without using a server.
There are many ways to make a contact form work without using a server. In this tutorial, we will use Google Sheets to store the data and Google App Script to make the API for the contact form if you love to make your own API.
Or you can use [Formspree](https://formspree.io/) to make your contact form work without using a server with just few clicks.  
But I will recommend you to make your own API because it will help you to learn how to make your own API.

## Steps to create your own working contact form without using a server

### Step 1 : Create a new Google Sheet

- Go to [Google Sheets](https://docs.google.com/spreadsheets/u/0/) and create a new Google Sheet.
- Rename the sheet to `Contact Form Responses `.
- Put the following headers in the first row of the sheet.

|   |     A     |   B   | C | ... |
|---|:---------:|:-----:|:-:|:---:|
| 1 | timestamp | email |   |     |

- You can add more headers if you want to store more data.

### Step 2: Create a new Google App Script

- Click on `Tools` and then click on `Script Editor`. or you can find the `Script Editor` in the `Add-ons` menu.
- You will see a new window open. It will ask you to give a name to your project. Give a name to your project as `Submit Form to Google Sheets` and click on `Create`.
- There will be a new file named `Code.gs` open in the editor.Remove all the code from the file and paste the following code in the file.

```js

var sheetName = 'Sheet1'
var scriptProp = PropertiesService.getScriptProperties()

function intialSetup () {
  var activeSpreadsheet = SpreadsheetApp.getActiveSpreadsheet()
  scriptProp.setProperty('key', activeSpreadsheet.getId())
}

function doPost (e) {
  var lock = LockService.getScriptLock()
  lock.tryLock(10000)

  try {
    var doc = SpreadsheetApp.openById(scriptProp.getProperty('key'))
    var sheet = doc.getSheetByName(sheetName)

    var headers = sheet.getRange(1, 1, 1, sheet.getLastColumn()).getValues()[0]
    var nextRow = sheet.getLastRow() + 1

    var newRow = headers.map(function(header) {
      return header === 'timestamp' ? new Date() : e.parameter[header]
    })

    sheet.getRange(nextRow, 1, 1, newRow.length).setValues([newRow])

    return ContentService
      .createTextOutput(JSON.stringify({ 'result': 'success', 'row': nextRow }))
      .setMimeType(ContentService.MimeType.JSON)
  }

  catch (e) {
    return ContentService
      .createTextOutput(JSON.stringify({ 'result': 'error', 'error': e }))
      .setMimeType(ContentService.MimeType.JSON)
  }

  finally {
    lock.releaseLock()
  }
}
```

- Now click on `File` and then click on `Save`. Give a name to your project as `Submit Form to Google Sheets` and click on `OK`.

### Step 3: Run the script

- Click on `Run` and then click on `Run function` and then click on `intialSetup`.
- It will ask you to give permission to the script. Click on `Review Permissions` and then click on `Allow`.(You can also click on `Advanced` and then click on `Go to Untitled Project (unsafe)` and then click on `Allow`.)

### Step 4: Creating new project trigger

- In the side menu you will find alarm clock icon which is called `Triggers`. Click on it.
- Click on `Add Trigger` and then click on `Select function` and then click on `doPost`.
- In the dropdowns select `doPost`
- Set the events fields to `From spreadsheet` and `On form submit`
- Then click `Save`


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/gs9dwm9qn2l4n46tfht2.png)





### Step 5: Publish the project as a web app

- Click on `Publish` and then click on `Deploy as web app`.
- Set `Project Version` to `New` and put `initial version` in the input field below.
- Set `Execute the app as` to `Me`.
- Set `Who has access to the app` to `Anyone`.
- Click on `Deploy`.
- You will see a new popup. Copy the `Current web app URL` .

### Simple Contact Form

- Create a new HTML file and paste the following code in it.
- Replace `scriptURL` with the `Current web app URL` you copied in the previous step.

```js
<form name="submit-to-google-sheet">
  <input name="email" type="email" placeholder="Email" required>
  <button type="submit">Send</button>
</form>

<script>
  const scriptURL = '<SCRIPT URL>'
  const form = document.forms['submit-to-google-sheet']

  form.addEventListener('submit', e => {
    e.preventDefault()
    fetch(scriptURL, { method: 'POST', body: new FormData(form)})
      .then(response => console.log('Success!', response))
      .catch(error => console.error('Error!', error.message))
  })
</script>
```

- You can add more input fields if you want to store more data.
- You can also add more headers in the Google Sheet if you want to store more data.
- `But make sure that the name of the input field and the header in the Google Sheet are same.`

## Conclusion

In this tutorial, we learned how to make a contact form that will work without using a server. We used Google Sheets to store the data and Google App Script to make the API for the contact form. You can also use [Formspree](https://formspree.io/) to make your contact form work without using a server with just few clicks.  
I hope you enjoyed this tutorial. If you have any questions, feel free to ask in the comments section below.  
And I know I am making continuous tutorials on Google App Script. But I will try to make tutorials on other topics also.😅