+++
categories = ["kubernetes", "k8s","GKE","Google Cloud Platform", "Google Container Engine", "Go", "golang"]
comments = true
date = "2017-08-17T13:15:50"
draft = true
showcomments = true
showpagemeta = true
slug = ""
tags = ["kubernetes", "Google Cloud Platform", "GCP"]
title = "Set up a simple Kubernetes cluster on Google Container Engine (GKE)"

+++
In this tutorial I will go over the basics of getting a simple Kubernetes cluser up and running in Google Container Engine. This tutorial assumes you are at least somewhat familiar with Docker.

For this tutorial I've created a very simple time JSON API that will be deployed on GKE. The code for this can be found [here] (https://github.com/zujko/container-engine-tutorial). I've written my app in Go but as long as you get your app running in Docker, it doesn't matter what your app is or what it is written in, you can deploy it with Kubernetes.

## Kubernetes

 
