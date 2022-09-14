---
title: "Easy way to Create your own API for FREE"
date: 2022-09-14T19:52:37+05:30
draft: false
cover: 
    image: https://res.cloudinary.com/practicaldev/image/fetch/s--9I6OhmbP--/c_imagga_scale,f_auto,fl_progressive,h_420,q_auto,w_1000/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/oy69l266lrci7i53zfuq.png
    alt: "Website"
    caption: "Web Projects for beginners"
editPost:
    URL: "https://github.com/Varshithvhegde/hugo-blog/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true
---


## Introduction

An application program interface (API) is a set of routines, protocols, and tools for building software applications. An API specifies how software components should interact. It can be used to create a new API or extend an existing API. An API can be entirely custom, specific to a component, or it can be designed based on an industry standard to ensure interoperability. An API can be entirely custom, specific to a component, or it can be designed based on an industry standard to ensure interoperability.

## What is Google Sheets?

[Google Sheets](https://docs.google.com/spreadsheets/u/0/) is a spreadsheet program included as part of a free, web-based software office suite offered by Google within its Google Drive service. It allows collaborative editing of spreadsheets online and offline, and the ability to store spreadsheets in the cloud. It is available as a web application, mobile app, and desktop app.

## How to create API using Google Sheets?

### Step 1
Open [Google Sheets](https://docs.google.com/spreadsheets/u/0/) and create a new spreadsheet.
### Step 2
Add the data you want to use in your API.
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/3hinnt2zcw25hf8g7rf2.png)
### Step 3
Click on the share button and share the spreadsheet with anyone with the link. **(Make sure you have selected the option to allow anyone with the link to view the spreadsheet)*
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/7ppcoxndkgdse92tlbis.png)
### Step 4
Now click on the help button and search for **AppScript** and click on it to open the AppScript editor.This will open a new tab in your browser.
### Step 5
This written code is the API for your spreadsheet. You can change the code to suit your needs. You can also add more functions to the code to make it more useful.For this tutorial, we will use the code given below.
```javascript
function doGet(req){
  var doc=SpreadsheetApp.getActiveSpreadsheet();
  var sheet=doc.getSheetByName('Sheet1');
  var values =  sheet.getDataRange().getValues();
  var output=[];
  for(var i=0;i<values.length;i++){
    var row={};
    row['Name']=values[i][0];
    row['Location']=values[i][1];
    output.push(row);
  }
  return ContentService.createTextOutput(JSON.stringify({data: output})).setMimeType(ContentService.MimeType.JSON);
}
```
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/b7hn3wca0zssc2su8mno.png)
### Step 6
Now click on **Deploy** and select **New Deployment**.

### Step 7
Now Select on the settings button .
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/45z39pfulg85b0wf87hf.png)

### Step 8

Now click on the **Web App** button and choose "Who has access to the app" as **Anyone** and click on **Deploy**.
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/rewk7ctk1ys42eqt6xzo.png)

### Step 9

It will ask you to authorize the app. Click on **Review Permissions** and click on **Allow**.
(It will say the website is not verified. Don't worry about that. It is safe to allow the app just click on **Advanced** and then click on **Go to App**)

### Step 10

Now you will get a URL. Copy the URL and paste it in your browser. You will get the data in JSON format.  
**Hurray🎉**! You have created your own API using Google Sheets.


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/zgwwg3sjpf7d59qa4zb3.png)

## Creating Sample Web Page to show the data

- Create a new file and name it **index.html**.
- Add the following code to the file.
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>Document</title>
</head>
<body>
	
</body>
<script>
  const api="YOUR_API_URL";
	fetch(api)
   .then(response => response.json())
   .then(characters => showCharacters(characters.data));
   showCharacters = characters => {
   
    document.write("<table class='tab'><tr class='tab'><th class='tab'><h2>Name</h2></th><th class='tab'><h2>USN</h2></th><th>");
    characters.forEach(character => {
		if(character.Name!="Name"){
      document.write("<tr style='color:black;font-weight: bold;'><td>" + character.Name + "</td><td class='tab'>" + character.Location + "</td><td>");
	  }
    });
}
</script>
</html>
```
- Be sure to replace **YOUR_API_URL** with the URL you got from the previous step.
- Now open the file in your browser and you will get the data in a table format.
- You can also use this API in your Android app or any other app.

## Conclusion

- In this tutorial, we learned how to create an API using Google Sheets.
- We also learned how to use the API in a web page.
- For reference, you can check out the [GitHub repository](https://github.com/Varshithvhegde/My_API) for this tutorial.  
  
If you have any doubts or suggestions, feel free to comment below.


