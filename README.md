# Cyberfiction - Interactive Scroll Website

This repository contains the source code for an interactive scroll-based website created using HTML, CSS, and JavaScript. The website uses GSAP and Locomotive Scroll to create smooth scrolling animations and interactive elements.




#Features


Smooth scrolling animations using Locomotive Scroll.
Interactive animations and transitions powered by GSAP.
Responsive design that adjusts to different screen sizes.
Canvas animation that scales images based on the scroll position.


#Installation
To run this project locally, follow these steps:

#Clone the repository: - git clone https://github.com/your-username/cyberfiction.git
Navigate to the project directory: - cd cyberfiction


#Usage


Scroll through the website to see the interactive animations.
The navigation bar remains fixed at the top of the page.
The content changes and transitions smoothly as you scroll.


Access images - https://drive.google.com/drive/folders/11xms0rv9kXrQBafK_H7J93nnW86MWbhX?usp=drive_link


Dependencies

Locomotive Scroll

GSAP (GreenSock Animation Platform)

ScrollTrigger (GSAP Plugin)

HTML

The HTML file includes the structure of the website, linking to external stylesheets and scripts, and defining the content and layout of the pages.

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cyberfiction</title>
    <link rel="stylesheet" href="style.css">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/locomotive-scroll@3.5.4/dist/locomotive-scroll.css">
</head>
<body>
    <div id="nav">
        <h3><b>Hey</b>Welcome*</h3>
        <button>JUNE,2024</button>
    </div>
    <div id="main">
        <!-- Content goes here -->
    </div>
    <script src="https://cdn.jsdelivr.net/npm/locomotive-scroll@3.5.4/dist/locomotive-scroll.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.11.5/gsap.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.11.5/ScrollTrigger.min.js"></script>
    <script src="script.js"></script>
</body>
</html>



JavaScript

The JavaScript file contains the functionality for smooth scrolling and animations using GSAP and Locomotive Scroll.

function locomotive() {
  gsap.registerPlugin(ScrollTrigger);

  const locoScroll = new LocomotiveScroll({
    el: document.querySelector("#main"),
    smooth: true,
  });
  locoScroll.on("scroll", ScrollTrigger.update);

  ScrollTrigger.scrollerProxy("#main", {
    scrollTop(value) {
      return arguments.length
        ? locoScroll.scrollTo(value, 0, 0)
        : locoScroll.scroll.instance.scroll.y;
    },
    getBoundingClientRect() {
      return {
        top: 0,
        left: 0,
        width: window.innerWidth,
        height: window.innerHeight,
      };
    },
    pinType: document.querySelector("#main").style.transform
      ? "transform"
      : "fixed",
  });
  ScrollTrigger.addEventListener("refresh", () => locoScroll.update());
  ScrollTrigger.refresh();
}
locomotive();

const canvas = document.querySelector("canvas");
const context = canvas.getContext("2d");

canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

window.addEventListener("resize", function () {
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;
  render();
});

function files(index) {
  var data = `
    ./male0001.png
    ./male0002.png
    ...
    ./male0299.png
  `;
  return data.split("\n")[index];
}

const frameCount = 300;

const images = [];
const imageSeq = { frame: 1 };

for (let i = 0; i < frameCount; i++) {
  const img = new Image();
  img.src = files(i);
  images.push(img);
}

gsap.to(imageSeq, {
  frame: frameCount - 1,
  snap: "frame",
  ease: `none`,
  scrollTrigger: {
    scrub: 0.15,
    trigger: `#page>canvas`,
    start: `top top`,
    end: `600% top`,
    scroller: `#main`,
  },
  onUpdate: render,
});

images[1].onload = render;

function render() {
  scaleImage(images[imageSeq.frame], context);
}

function scaleImage(img, ctx) {
  var canvas = ctx.canvas;
  var hRatio = canvas.width / img.width;
  var vRatio = canvas.height / img.height;
  var ratio = Math.max(hRatio, vRatio);
  var centerShift_x = (canvas.width - img.width * ratio) / 2;
  var centerShift_y = (canvas.height - img.height * ratio) / 2;
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  ctx.drawImage(
    img,
    0,
    0,
    img.width,
    img.height,
    centerShift_x,
    centerShift_y,
    img.width * ratio,
    img.height * ratio
  );
}

ScrollTrigger.create({
  trigger: "#page>canvas",
  pin: true,
  scroller: `#main`,
  start: `top top`,
  end: `600% top`,
});

gsap.to("#page1", {
  scrollTrigger: {
    trigger: `#page1`,
    start: `top top`,
    end: `bottom top`,
    pin: true,
    scroller: `#main`,
  }
});

gsap.to("#page2", {
  scrollTrigger: {
    trigger: `#page2`,
    start: `top top`,
    end: `bottom top`,
    pin: true,
    scroller: `#main`,
  }
});

gsap.to("#page3", {
  scrollTrigger: {
    trigger: `#page3`,
    start: `top top`,
    end: `bottom top`,
    pin: true,
    scroller: `#main`,
  }
});



