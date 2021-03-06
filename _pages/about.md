---
permalink: /
title: "About me"
excerpt: "About me"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

{% include base_path %}

Welcome to my personal website! My name is Hao He (何昊). I'm currently a Ph.D. candidate in Computer Software and Theory at Peking University, supervised by [Minghui Zhou](http://sei.pku.edu.cn/~zhmh/). Before that, I received my Bachelors' Degree on Computer Science at Peking University in 2020.  My research interest is to address practical problems and interpret interesting phenomenon in the field of software engineering, using whatever methodology that helps, be it quantitative or qualitative. 

Recently, I'm focusing on the general topic of dependency management in software engineering. More specifically, I want to design novel tools to manage, curate and secure software dependencies during software evolution. I have developed an [approach](/publication/2021-recommending-library-migration) for automated mining and recommendation of library migration targets, which have been deployed in a proprietary 3rd-party library management tool at Huawei. I am also participating a side research project in understanding code comment practices.

Besides that, I also love to make something cool by programming. I also enjoy playing games, especially those with complex and in-depth mechanics to study.

For my detailed information please see below. You can also refer to my [GitHub](https://github.com/hehao98) for paper code and other projects.

## Education

* B.S. in Computer Science, Peking University, 2016-2020, GPA 3.70/4.0 (Top 20%), [Thesis](https://hehao98.github.io/files/2020-bachelor-thesis.pdf).
* Ph.D. Candidate in Computer Software and Theory, Peking University, 2020-2025 (expected). Advisor: [Minghui Zhou](http://sei.pku.edu.cn/~zhmh/).

## Publications

  <ul>{% for post in site.publications reversed %}
    {% include archive-single-cv.html %}
  {% endfor %}</ul>

## Working Experience

* **Sept 2020 - Jan 2021, Software Engineer Intern**
  * Software Analysis Lab, Cloud BU, Huawei Technologies Co., Ltd.
  * Responsible for developing Spark™ applications for large-scale mining of internal Java projects, and using the mined data for 3rd-party library risk prediction and migration recommendation.

## Teaching Experience

<ul>{% for post in site.teaching reversed %}
   {% include archive-single-cv.html %}
 {% endfor %}</ul>

## Patents

* Xiao Cheng, Zeyu Wang, Ruowen Chen, Junjie Yu, <b>Hao He</b>, Guangtai Liang, Minghui Zhou. A Service that Upgrades or Replaces Vulnerable Thrid-Party Libraries Automatically (一个漏洞三方库自动升级替换服务). Huawei Technologies Co., Ltd. 

## Awards and Honors

* 2020 ChinaSoft Software Prototype Contest (Free Topic Track), Thrid Prize
* The Third Prize of Peking University Scholarship, 2018-2019
* Award for Academic Excellence, Peking University, 2018-2019
* Award for Academic Excellence, Peking University, 2017-2018

## Skills

* Language
  * Chinese (Native) 
  * English (Fluent), TOFEL 106/120, CET-6 661/710
  * Japanese (Fluent), JLPT N2 Qualified 180/180 (yes, a full score)
* Programming Languages
  *  C, Python, C++, C#, Java, JavaScript
* Skills for 
  * Program Analysis and Mining Software Repositories
  * Data Analysis: Numpy, Pandas, Matplotlib, Seaborn
  * Frontend: HTML, CSS, Vue.js, Bootstrap, Element UI
  * Backend: Spring Boot, MongoDB, MySQL, Spark, Hadoop, MapReduce
  * Game Development: Unity, Cocos Creator, OpenGL

## Some Course Projects

<ul>{% for post in site.portfolio %}
  {% if post.project_type == "course_project" reversed %}
    {% include archive-single-cv.html %}
  {% endif %}
{% endfor %}</ul>



