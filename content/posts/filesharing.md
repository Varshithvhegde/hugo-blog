---
title: "How I Created a File Sharing Website using Simple JavaScript"
date: 2022-10-24T09:13:56+05:30
draft: false
cover: 
    image: https://res.cloudinary.com/practicaldev/image/fetch/s--pQuCg7vT--/c_imagga_scale,f_auto,fl_progressive,h_420,q_auto,w_1000/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ya3ddwr0o085d8ikmil4.png
    alt: "Website"
    caption: "Web Projects for beginners"
editPost:
    URL: "https://github.com/Varshithvhegde/hugo-blog/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true
---
Any Share is a simple, lightweight, and fast file sharing service. It is written in Javascript and uses the [Firebase](https://firebase.google.com/) platform.  
Website I created for secure file sharing with friends and family.  
You can Create your own website with this code.

## Features

-   Upload files
-   Download files
-   Delete files
-   Share files
-   View files
-   Secure file sharing

## Working

- Any Share uses Firebase to store files. It uses Firebase Storage to store files and Firebase Realtime Database to store metadata of files. 
- When a file is uploaded, it is stored in Firebase Storage and a unique ID is generated for the file. This ID is used to access the file. 
- The metadata of the file is stored in Firebase Realtime Database. This metadata includes the url to the file and the unique ID of the file.
- When a file is shared, the unique ID of the file is shared. This ID is used to access the file.
- Receiver of the file can access the file using the unique ID of the file.
- When the file is received by the receiver using the unique ID, the file is downloaded from Firebase Storage and displayed to the receiver.
- Once the file is received by the receiver, the file is automatically deleted from Firebase Storage.
- This way the file is shared securely.

## How to use

<a href="https://anyshare.vercel.app"><img src="https://user-images.githubusercontent.com/80502833/193975789-641c7b56-d7b6-474a-9082-b52335d21c22.png" width=300px height=400px align="center"/></a>
<!-- ![frame_generic_dark (12)](https://user-images.githubusercontent.com/80502833/193975789-641c7b56-d7b6-474a-9082-b52335d21c22.png) -->



- Visit [Any Share](https://anyshare.vercel.app/).
- Upload a file.
- Wait for the file to be uploaded.
- Share the unique ID of the file with the receiver.
- Receiver can access the file using the unique ID of the file.
- Once the file is received by the receiver, the file is automatically deleted from Firebase Storage.

## Code Review

- Code for Firebase storage uploading

```javascript
function uploadFile() {
    if(document.getElementById("file").value != ""){
    var uploadtext = document.getElementById("upload").innerHTML;
  document.getElementById("upload").innerHTML = "Uploading...";
  var file = document.getElementById("file").files[0];
  var storageRef = firebase.storage().ref("images/" + file.name);
  var uploadTask = storageRef.put(file);
  uploadTask.on('state_changed', function (snapshot) {
    var progress = (snapshot.bytesTransferred / snapshot.totalBytes) * 100;
    console.log('Upload is ' + progress + '% done');
  }, function (error) {
    console.log(error.message);
    document.getElementById("upload").innerHTML = "Upload Failed";
  }, function () {
    
    
    uploadTask.snapshot.ref.getDownloadURL().then(function (downloadURL) {
      console.log('File available at', downloadURL);
      saveMessage(downloadURL);
    });
  });
}
else{
    var uploadtext = document.getElementById("upload").innerHTML;
    document.getElementById("upload").innerHTML = "Please select a file";
    // After 2 sec make it empty
    setTimeout(function(){
        document.getElementById("upload").innerHTML = uploadtext;
    }
    , 2000);
}
}

```

- Code for Firebase storage downloading

```javascript
function showfile(){
var uniqueId= document.getElementById("unique").value;
    if(uniqueId==""){
        alert("Unique Id is empty\n Please enter a Unique Id");
        return;
    }
    var ref = firebase.database().ref("image");
    var flag = 0;
    ref.on("value", function(snapshot) {
        snapshot.forEach(function(childSnapshot) {
        var childData = childSnapshot.val();
        if (childData.number == uniqueId){
        
        flag = 1;
        window.open(childData.url, "_blank");
        // AFter this delete the image from the database
        ref.child(childSnapshot.key).remove();
        // Remove file from storage
        //Run this with 5sec delay
        setTimeout(function(){
        var storageRef = firebase.storage().refFromURL(childData.url);
        storageRef.delete().then(function() {
             ref.child(childSnapshot.key).remove();
        // File deleted successfully
        }).catch(function(error) {
        
        });
        }, 15000);

        
        }
        });
    }
    );
}
```


- Generated unique ID

```javascript

function createUniquenumber(){
    // Create a unique 5 digit number for each image which is not in the database field number yet
    var number = Math.floor(10000 + Math.random() * 90000);
    var ref = firebase.database().ref("image");
    ref.on("value", function(snapshot) {
        snapshot.forEach(function(childSnapshot) {
        var childData = childSnapshot.val();
        if (childData.number == number){
            createUniquenumber();
        }
        });
    });
    return number;
    

}
```

- Code for saving metadata of file in Firebase Realtime Database

```javascript
function saveMessage(downloadURL) {
    var newMessageRef = messagesRef.push();
    var unique= createUniquenumber();
    // Hidding recive file div
    var x = document.getElementById("downloadiv");
    x.style.display = "none";
    var showUnique = document.getElementById("ShowUniqueID");
    var shU=document.getElementById("showunique");
    shU.value=unique;
    showUnique.style.display = "block";
   
    newMessageRef.set({
        url: downloadURL,
        number: unique
    });
    document.getElementById("upload").innerHTML = "Upload Successful";
    //Make file input empty
    document.getElementById("file").value = "";
   
    }
```

## Conclusion

- In this tutorial I have explained how I created my own File Sharing Web App.

## References

- [Github Code](https://github.com/Varshithvhegde/anyshare)
- [Firebase Storage](https://firebase.google.com/docs/storage)
- [Firebase Documentation](https://firebase.google.com/docs)


