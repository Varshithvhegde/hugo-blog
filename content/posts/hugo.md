---
title: "Build Portfolio Website with Hugo"
date: 2022-08-14T20:29:28+05:30
draft: false
cover: 
    image: https://res.cloudinary.com/practicaldev/image/fetch/s--aVvwgF2Q--/c_imagga_scale,f_auto,fl_progressive,h_420,q_auto,w_1000/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/an647cem25bfc52mctxp.png
    alt: "Website"
    caption: "Beautiful Website"
editPost:
    URL: "https://github.com/Varshithvhegde/hugo-blog/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true
---

A personal webpage is a perfect place to let the world know about you and showcase your past accomplishments. Put your resume, your projects, your blogs in with a personalized theme which makes people know you have a great taste: all-in-one! It’s your portfolio displayed online, a small yet cool project you can do with not much effort, why not?

With Github Pages, we can host a personal webpage without bothering about finding a domain name, and with Hugo, we have a variety of themes to choose from. Now, let's start this step-by-step tutorial to set up your personal webpage!

## Introduction to HUGO and GitPage

Hugo is one of the most popular open-source static site generators and is written in GO. ItΓÇÖs simple, efficient, easy to scale and fast to deploy. Simply install with brew, clone themes you like from Github or the official website [HUGO](https://gohugo.io/), make some changes in the configuration file and deploy, then your page will be online.

[Github Pages](https://pages.github.com/) is a static web hosting service provided by Github, which provides 1GB of free space and provides convenient deployment directly through the Github repository.

This site uses Hugo and Github Pages to create and deploy. The following briefly introduces the deployment process.

## Installation

**Install Hugo**

Open your terminal, run the following command-line one by one:
- MacOS:   
```
brew install hugo
```
- Linux:
```
sudo apt install hugo
```
- Windows:
```
scoop install hugo
```

To check whether you installed Hugo successfully, enter the following into your terminal

    hugo version
## Configuration

    hugo new my-website
    cd my-website
    hugo
## Deployment
- Github Pages: 
  Open your terminal, run the following command-line one by one:
```
    hugo
    git add .
    git commit -m "update"
    git push origin master
    git push pages master
    cd ..
    rm -rf my-website
```
- MacOS:
```
    open http://localhost:1313
```
- Linux:
```
    firefox http://localhost:1313
```
- Windows:
```
    start http://localhost:1313
```
## Conclusion
Congratulations! You have successfully set up a personal webpage with Hugo and Github Pages.

## References
- [HUGO](https://gohugo.io/): Hugo is a static site generator written in Go.
- [Github Pages](https://pages.github.com/): Github Pages is a static web hosting service provided by Github, which provides 1GB of free space and provides convenient deployment directly through the Github repository.

## Examples
- [Blog Site](https://github.com/Varshithvhegde/hugo-blog)
- [Portfolio Site](https://hugo-alexa-portfolio.netlify.app/)
