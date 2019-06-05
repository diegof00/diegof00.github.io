##Delete containers by image name

{% highlight java %}
sudo  docker ps -a | awk '{ print $1,$2 }' | grep sozpinar/consul-imex | awk '{print $1 }' | xargs -I {} sudo docker rm {}
{% endhighlight %}
