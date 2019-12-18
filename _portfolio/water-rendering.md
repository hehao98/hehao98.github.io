---
title: "Water Rendering"
excerpt: "Implementation of Water Rendering Techniques"
collection: portfolio
---

I started this personal project both out of my personal interest on computer graphics and practice of OpenGL and C++ programming. I choose to implement water rendering becauce I love water! Personally I enjoy swimming and I've found that the color, wave and lighting of water is beautiful. That's why I choose to implement techniques for rendering water.

This project is based on OpenGL and C++. The scene consists of one skybox, and a water surface. The water surface is just many small squares that constitue a surface, and the height of each vertex is modified to simulate waves. For wave simulation, I have implemented Gestner waves and an FFT based wave function from the famous 2002 SIGGRAPH paper "Simulating Ocean Water". It is implemented on CPU. I have not tried a version on GPU, which will be much faster.

Here are some of my results. The source code is hosted on [GitHub](https://github.com/hehao98/WaterRendering)

![Lighting]({{ site.url }}/assets/ocean-pic/ocean.gif)
![Lighting]({{ site.url }}/assets/ocean-pic/ocean2.gif)
![Lighting]({{ site.url }}/assets/ocean-pic/ocean3.gif)
![Lighting]({{ site.url }}/assets/ocean-pic/ocean4.gif)
![Lighting]({{ site.url }}/assets/ocean-pic/ocean5.gif)
![Lighting]({{ site.url }}/assets/ocean-pic/ocean6.gif)
![Lighting]({{ site.url }}/assets/ocean-pic/ocean7.gif)
![Lighting]({{ site.url }}/assets/ocean-pic/ocean8.gif)
![Lighting]({{ site.url }}/assets/ocean-pic/ocean9.gif)


