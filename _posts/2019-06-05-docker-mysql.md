---
layout: post
title: "Docker Mysql container"
description: "docker mysql"
tags: [examples, docker]
categories: [docker]
---

## Create and run a docker container with MYSQL 

{% highlight java %}

  docker run --name mysql_1 -d --env="MYSQL_ROOT_PASSWORD=root" -p 3306:3306 mysql:5.7
  
{% endhighlight %}

## Enter to mysql bash

{% highlight java %}

	docker exec -it mysql_1 mysql -u root -p
    
{% endhighlight %}

## Create Backup

{% highlight java %}

	docker exec mysql_1 /usr/bin/mysqldump -u root --password=root DATABASE > my_backup.sql
    
{% endhighlight %}

## Restore

{% highlight java %}

	cat my_backup.sql | docker exec -i mysql_1 /usr/bin/mysql -u root --password=root DATABASE
    
{% endhighlight %}



> https://gist.github.com/spalladino/6d981f7b33f6e0afe6bb

