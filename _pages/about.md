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

Welcome to my personal website! My name is Hao He (何昊). I'm currently a PhD candidate in Computer Software and Theory at Peking University, supervised by [Minghui Zhou](http://sei.pku.edu.cn/~zhmh/). Before that, I received my Bachelors' Degree on Computer Science in 2020.  My research interest is to address practical problems and interpret interesting phenomenons in the field of software engineering, using whatever methodology that helps, be it quantitative or qualitative. 

Besides that, I also love to make something cool by programming. I also enjoy playing games, especially those with complex and in-depth mechanics to study.

For my detailed information please see below. You can also refer to my [GitHub](https://github.com/hehao98) for paper code and other projects.

## Education

* B.S. in Computer Science, Peking University, 2016-2020, GPA 3.70/4.0 (Top 20%)
* PhD Candidate in Computer Software and Theory, Peking University, 2020-2025 (expected). Supervisor: [Minghui Zhou](http://sei.pku.edu.cn/~zhmh/)

## Publications

  <ul>{% for post in site.publications reversed %}
    {% include archive-single-cv.html %}
  {% endfor %}</ul>

## Working Experience

* **Software Engineer Intern, September 2020 - December 2021 (expected)**
  * Software Analysis Lab, Cloud BU, Huawei Technologies Co., Ltd.
  * Responsible for developing and deploying Spark™ applications for large-scale mining of internal Java projects, and use the mined data for 3rd-party library risk prediction and migration recommendation.

## Research Projects

<ul>{% for post in site.portfolio reversed %}
  {% if post.project_type == "research_project" %}
    {% include archive-single-cv.html %}
  {% endif %}
{% endfor %}</ul>

## Teaching Experience

<ul>{% for post in site.teaching reversed %}
   {% include archive-single-cv.html %}
 {% endfor %}</ul>

## Patents

* Xiao Cheng, Zeyu Wangm, Ruowen Chen, Junjie Yu, <b>Hao He</b>, Guangtai Liang, Minghui Zhou. A Service that Upgrades or Replaces Vulnerable Thrid-Party Libraries Automatically (一个漏洞三方库自动升级替换服务). Huawei Technologies Co., Ltd. 

## Awards and Honors

* 2020 ChinaSoft Software Prototype Contest (Free Topic Track), Thrid Prize
* The Third Prize of Peking University Scholarship, 2018-2019
* Award for Academic Excellence, Peking University, 2018-2019
* Award for Academic Excellence, Peking University, 2017-2018

## Skills

* Language
  * Chinese (Native) 
  * English (Fluent), TOFEL 106/120, CET-6 661/710
  * Japanese (Fluent), I want to take JLPT N1 this year but the pandemic stops me QAQ
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



