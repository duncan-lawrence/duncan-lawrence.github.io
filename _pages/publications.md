---
layout: page
permalink: /publications/
title: publications
description:
nav: true
nav_order: 2
---

<!-- _pages/publications.md -->

<div class="publications">

<h2 class="bibliography">Journal Articles</h2>

{% bibliography --query @article %}

<h2 class="bibliography">Unpublished</h2>

{% bibliography --query @unpublished %}

</div>
