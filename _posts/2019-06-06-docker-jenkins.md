---
layout: post
title: "Docker Jenkins"
description: "docker jenkins"
tags: [docker, jenkins, ci]
categories: [docker, jenkins]
---

## Create jenkins container

  sudo docker run --rm -u root -p 9191:8080 -v "$PWD":/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock jenkinsci/blueocean
