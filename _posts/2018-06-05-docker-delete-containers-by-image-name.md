---
layout: post
title: "Delete docker containers by image name"
description: "docker delete containers by image name"
tags: [docker]
categories: [docker]
---

## Delete containers by image name

{% highlight java %}
sudo  docker ps -a | awk '{ print $1,$2 }' | grep sozpinar/consul-imex | awk '{print $1 }' | xargs -I {} sudo docker rm {}
{% endhighlight %}
