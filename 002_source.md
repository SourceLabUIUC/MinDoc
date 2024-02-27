---
layout: default
title: The Source
number: 002
---

# The Source

MY WONDEFUL SOURCES part 2
<!-- <iframe width="420" height="315" src="https://www.youtube.com/watch?v=EmSrQCDsMv4&t=1282s&ab_channel=BillRaymond" frameborder="0" ></iframe> -->

{% assign media = site.mindoc_media | sort: "order" | where_exp: "item", "item.page == 'source'" | where_exp: "item", "item.media_type == 'image'" %}

{% include media.html pages=media %}

{% assign media = site.mindoc_media | sort: "order" | where_exp: "item", "item.page == 'source'" | where_exp: "item", "item.media_type == 'video'" %}

{% include media.html pages=media %}




