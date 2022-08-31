---
title: "Create Your Own Live Web Editor using HTML, CSS, and JavaScript"
date: 2022-08-31T20:52:49+05:30
draft: false
cover: 
    image: https://res.cloudinary.com/practicaldev/image/fetch/s--cZTZkaov--/c_imagga_scale,f_auto,fl_progressive,h_420,q_auto,w_1000/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/q9xabpbas9i9n1qhntz3.png
    alt: "Website"
    caption: "Custom Code Editor"
editPost:
    URL: "https://github.com/Varshithvhegde/hugo-blog/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true
---

## Introduction

In this tutorial, we will be creating a live web editor. This is a web application that allows you to write HTML, CSS, and JavaScript code and see the results in real time. This is a great tool for learning web development and for testing out code snippets. We will be using the [iframe](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe) element to display the results. The iframe element is used to embed another document within the current HTML document. The src attribute of the iframe element specifies the URL of the document to embed.

## What is a Web Editor?

A web editor is a web application that allows you to write HTML, CSS, and JavaScript code and see the results in real time. Uses of a web editor include: Fast prototyping, Easy testing, and Learning web development.

## What is a Live Web Editor?

A live web editor is a web editor that displays the results of the code in real time. 

## Prerequisites   

Before you begin this tutorial, you should have a basic understanding of HTML, CSS, and JavaScript. You should also have a basic understanding of the DOM and how to select elements using JavaScript. Finally, you should have a basic understanding of the iframe element.

Software you will need:
- A code editor (Visual Studio Code, Sublime Text, Atom, etc.)
-  A web browser (Google Chrome, Mozilla Firefox, Microsoft Edge, etc.)
-  A browser extension for live preview (Live Server, Live Preview, etc.)
-  Github 
-  Github Pages for hosting

## Step 1: Create the HTML File

Create a new folder and name it "live-web-editor". Inside the folder, create a new file and name it "**index.html**". Open the file in your code editor and add the following code:

```html
<!DOCTYPE html>
 <html>
 <head>
 	<title>Real-Time Editor</title>
 	<link rel="stylesheet" type="text/css" href="styles.css">
 	<script defer type="text/javascript" src="app.js"></script>
 	<!-- <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script> -->
	<script src="https://cdnjs.cloudflare.com/ajax/libs/split.js/1.0.0/split.min.js" integrity="sha512-tTsZnBXEzNdEaqUO9Ok8fUofS73xieiBa54pD/sxOSvayIgItM9MmEM0CnUjA13LDnJT22sfwmjf20+Bo2174g==" crossorigin="anonymous"></script>
 </head>
 <body>
 	<div class="container split">
		<!-- Text area for Html Code  -->
 		<textarea id="htmlCode"  placeholder="Type HTML code here" spellcheck="false" oninput="update(0)" onkeydown="if(event.keyCode===9){var v=this.value,s=this.selectionStart,e=this.selectionEnd;this.value=v.substring(0, s)+'\t'+v.substring(e);this.selectionStart=this.selectionEnd=s+1;return false;}if(event.keyCode==8){update(1);}"></textarea>
 		<!-- Text area for Css Code  -->
		<textarea id="cssCode"  placeholder="Type CSS code here" spellcheck="false" oninput="update(0)" onkeydown="if(event.keyCode===9){var v=this.value,s=this.selectionStart,e=this.selectionEnd;this.value=v.substring(0, s)+'\t'+v.substring(e);this.selectionStart=this.selectionEnd=s+1;return false;}if(event.keyCode==8){update(1);}"></textarea>
 		<!-- Text area for Javascript Code  -->
		<textarea id="javascriptCode" spellcheck="false" placeholder="Type JavaScript code here" oninput="update(0)" onkeydown="if(event.keyCode===9){var v=this.value,s=this.selectionStart,e=this.selectionEnd;this.value=v.substring(0, s)+'\t'+v.substring(e);this.selectionStart=this.selectionEnd=s+1;return false;}if(event.keyCode==8){update(1);}"></textarea>
 	</div>
 	<div class="iframe-container split">
 		<iframe id="viewer"></iframe>
 	</div>
	
 </body>
 </html>

 ```
 For Explanation of the code
 ```javascript
 onkeydown="if(event.keyCode===9){var v=this.value,s=this.selectionStart,e=this.selectionEnd;this.value=v.substring(0, s)+'\t'+v.substring(e);this.selectionStart=this.selectionEnd=s+1;return false;}if(event.keyCode==8){update(1);}
 ```
 Above code is used for live rendering of textarea it will automatically render when you type in textarea and also is used enable tab in textarea because by default tab is not enabled in textarea.

## Step 2: Create the CSS File

Create a new file and name it "**styles.css**". Open the file in your code editor and add the following code:

```css
@import url('https://fonts.googleapis.com/css2?family=Open+Sans&display=swap');

*{
	padding: 0;
	margin: 0;
	box-sizing: border-box;
}

body{
	height: 100vh;
	display: flex;
}
.container{
	background: #E7E7E7;
	display: flex;
	flex-direction: column;
	width: 50%;
	height: 100vh;
	margin: 3px;

}
.container textarea {
	background-color:  #121212;
	border:1px solid #0dddf0;
	resize: none;
	width: 100%;
	height: 33.333%;
	font-size: 1.4rem;
	padding: 10px;
	resize: vertical;
	overflow-y: scroll;
	color:white;
}
.container textarea:focus {
	outline: none;
	color:white;
}
.iframe-container{
	background: white;
	width: 50%;
	height: 100vh;
	margin: 3px;
}
#viewer{
	width: 100%;
	height: 100%;
}
.split {
  width:100%;
  height:100%;
}
.gutter {
  cursor: e-resize;
  height: 100%;
  background: grey;
}
.gutter.gutter-horizontal {
    cursor: ew-resize;
}
```

## Step 3: Create the JavaScript File

Create a new file and name it "**app.js**". Open the file in your code editor and add the following code:

```javascript
var j=0;
//Function for live Rendering
function update(i) {
	if(i==0){
	let htmlCode=document.getElementById("htmlCode").value;
	let cssCode=document.getElementById("cssCode").value;
	let javascriptCode=document.getElementById("javascriptCode").value;
	let text=htmlCode+"<style>"+cssCode+"</style>"+"<scri"+"pt>"+javascriptCode+"</scri"+"pt>";
	let iframe=document.getElementById('viewer').contentWindow.document;
	iframe.open();
	iframe.write(text);
	iframe.close();
	}

	else if(i==1){
		
		let htmlCode=document.getElementById("htmlCode").value;
		let html=htmlCode.slice(0,htmlCode.length);
		document.getElementById("htmlCode").value=html;
		j=1;

	}
```

For Explanation of the code below line takes the value of textarea and store it in variable 

```javascript
let text=htmlCode+"<style>"+cssCode+"</style>"+"<scri"+"pt>"+javascriptCode+"</scri"+"pt>";
```

## Step 4 : Running the Project

Save all the files and open the "**index.html**" file in your browser using the live server extension. You should see the following output:

![Html Editor](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/xgbxaky2193t5b5l6mjo.png)


## Step 5 : Try it out

Now you can try out your own code in the text area and see the output in the iframe.
You can also test live rendering by deleting the code in the text area and see the output in the iframe.



## Resources

- [Varshith V Hegde](https://github.com/VarshithVHegde/htmleditor)
- [Live Demo](https://Varshithvhegde.gitub.io/htmleditor)

## Demo

- [Live Demo](https://Varshithvhegde.gitub.io/htmleditor)


## Improvements

You can improve this code editor by adding more features like:
- Adding a button to download the code as a zip file.
- Added auto-complete feature for HTML, CSS, and JavaScript.
- Added auto tag closing feature for HTML.(I have already added this feature in my code editor check it out [here](https://github.com/VarshithVHegde/htmleditor))
- Added a button to clear the code editor.
- Added a button to change the theme of the code editor.
- Added a button to change the font size of the code editor.

## Conclusion

In this tutorial, you learned how to create a live code editor using HTML, CSS, and JavaScript. You also learned how to use the split.js library to create a split screen layout. You can use this code editor to test your HTML, CSS, and JavaScript code. You can also use this code editor to create your own website.


## Author

- [Varshith V Hegde](https://github.com/VarshithVHegde)
- [Portfolio](https://varshithvhegde.github.io)




