---
title: "How I Created Augmented Reality(AR) Web App using Only HTML"
date: 2022-10-24T09:22:37+05:30
draft: false
cover: 
    image: https://res.cloudinary.com/practicaldev/image/fetch/s--9cMaLeF2--/c_imagga_scale,f_auto,fl_progressive,h_420,q_auto,w_1000/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/h5r4n8onag4wxnsggsck.png
    alt: "Website"
    caption: "Web App for sharing files"
editPost:
    URL: "https://github.com/Varshithvhegde/hugo-blog/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true
---
## What is Augmented Reality(AR)?

Augmented Reality(AR) is a technology that superimposes a computer-generated image on a user's view of the real world, thus providing a composite view. It is related to a more general concept called mediated reality, in which a view of reality is modified (possibly even diminished rather than augmented) by a computer. As a result, the technology functions by enhancing one's current perception of reality. AR can be defined as a system that fulfills the following criteria simultaneously:

- The system must be able to perceive its environment. 
- The system must be able to analyze or process the information it perceives.

## Why I Created Augmented Reality(AR) Web App?

I working on an AR furniture App called [Touch Reno](https://touchreno.netlify.com/) and it was like a startup.  
When we pitched our idea to the investors, they were like "It's a great idea but we don't have any idea how it works".  
So I decided to create a simple AR Web App to show them how it works.
So that they can view what is AR without actually downloading any app.

## How to Create?

- After some intensive research, I found that [AR.js](https://ar-js-org.github.io/AR.js-Docs/)
- It uses [A-Frame](https://aframe.io/) which is a web framework for building virtual reality experiences.
- Main part of this AR.js marker.
- Marker is a pattern that is recognized by the AR.js library. It is a pattern that is printed on a paper and then it is used to recognize the object in the real world.

## Working 

- First, we need to create a marker. or just download from here [Marker](https://github.com/Varshithvhegde/Arweb#readme)

### Step 1

- Create a new file and name it index.html
- Add the following code to the file

```html
<!doctype HTML>
<html>
<style lang="en" type="text/css" id="night-mode-pro-style">
    body {
        background-color: transparent;
    }
</style>
<link type="text/css" rel="stylesheet" id="night-mode-pro-link">

<head>
    <title>AR</title>
    <link rel="shortcut icon" href="https://img.icons8.com/fluency/344/augmented-reality.png" type="image/x-icon">
    <meta name="viewport" content="width=device-width, user-scalable=yes, minimum-scale=1.0, maximum-scale=1.0">
    <script src="https://aframe.io/releases/0.9.2/aframe.min.js"></script>
    <script src="https://raw.githack.com/jeromeetienne/AR.js/master/aframe/build/aframe-ar.min.js"></script>
    <script src="https://raw.githack.com/donmccurdy/aframe-extras/master/dist/aframe-extras.loaders.min.js"></script>
</head>
<!--  https://raw.githubusercontent.com/nicolocarpignoli/nicolocarpignoli.github.io/master/ar-playground/models/CesiumMan.gltf-->
<body>
    <a-scene embedded arjs="detectionMode: mono_and_matrix; matrixCodeType: 3x3;">
        <!-- include assets like 3D models and give them an id to use later -->
        <a-assets>
            <a-assets-item id="dinosaur"
                src="https://raw.githack.com/AR-js-org/AR.js/master/aframe/examples/image-tracking/nft/trex/scene.gltf">
            </a-assets-item>
            <a-assets-item id="robot"
                src="https://raw.githubusercontent.com/nicolocarpignoli/nicolocarpignoli.github.io/master/ar-playground/models/CesiumMan.gltf">
            </a-assets-item>
            
        </a-assets>
        <!-- recognise different barcode markers ad show digital objects - box/sphere/cylinder/3D-model/image/video/anything -->
        <a-marker type="barcode" value="0">
            <!-- <a-box material="color: red;" scale="0.5 0.5 0.5"></a-box> -->
            <a-entity position="0 0 0" scale="1 1 1" rotation="0 0 0" animation-mixer gltf-model="#robot"></a-entity>
        </a-marker>
        <a-marker type="barcode" value="1">
            <a-entity position="0 0 0" scale="1 1 1" rotation="0 0 0" animation-mixer gltf-model="#robot"></a-entity>
        </a-marker>
        <a-marker type="barcode" value="2">
            <a-cylinder color="#FFC65D" scale="0.5 0.5 0.5"></a-cylinder>
        </a-marker>
        <a-marker type="barcode" value="3">
            <a-entity position="0 0 0" scale="0.06 0.06 0.06" rotation="0 90 0" gltf-model="#dinosaur"></a-entity>
        </a-marker>
        <!-- adding the camera -->
        <a-entity camera></a-entity>
    </a-scene>
</body>

</html>
```

- Here we are using a-scene tag which is a container for all the 3D objects in the scene.
- We are using a-marker tag which is used to detect the marker.
- We are using a-assets tag which is used to load the 3D models.
- We are using a-entity tag which is used to add the 3D models to the scene.
- We are using a-camera tag which is used to add the camera to the scene.
- We are using a-box tag which is used to add the box to the scene.
- We are using a-cylinder tag which is used to add the cylinder to the scene.


### Step 2

- Just save the file and open it in the browser.
- Download the [Marker](https://github.com/Varshithvhegde/Arweb#readme) and print it.
- Then focus the camera on the marker and you will see the 3D model.

### Demo Video

{% embed https://user-images.githubusercontent.com/80502833/197395745-2a871851-00b1-4da5-92fc-5b9ce567150a.mp4 %}

## Conclusion

- I hope you enjoyed this tutorial. If you have any questions, feel free to ask in the comments section below.
- Comment your thoughts and suggestions below.
- Code is available on my Github
{% embed https://github.com/Varshithvhegde/Arweb %}
- For Live Demo [Click Here](https://varshithvhegde.github.io/Arweb)
