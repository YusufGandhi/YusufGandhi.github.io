---
layout: post
title:  "Setting up GPU instances on AWS"
permalink: gpu-aws
---
> **UPDATE 23-Aug-2016**: The link below turns out to be for CUDA 6.5. If you want to install CUDA 7.5 (which is required by Matlab 2016A), please go to [this page](http://tleyden.github.io/blog/2015/11/22/cuda-7-dot-5-on-aws-gpu-instance-running-ubuntu-14-dot-04/) instead.

As I'm finishing my degree at ANU, I am required to write a thesis. My topic is about deep learning for  image classification. To achieve this, I need to train three different autoencoders on three different image channels. This will set the foundation of the next phase, training the convolutional neural networks to do classification.

The chosen tool is MATLAB 2016A due to its convenience to use and robustness. (I actually considered other open-source frameworks, i.e. TensorFlow or Theano, but MATLAB is preferred by my supervisor.) However, for training this stuff, MATLAB 2016A, unfortunately, requires GPU-powered machines. And, to make things worse, my current scholarship sponsor forbids "buying" anything related to research. We're just allowed to "rent" stuff. Regardless of the rules are so weird, rules are rules. Just need to obey them to stay alive.

Long story short, I chose to use Amazon Web Services as they provide a couple of GPU instance types, i.e.  the g2.2xlarge instance and the g2.8xlarge instance. The differences are the size of the memory and storage spaces, not sure whether the GPUs are the same though. On AWS instances, you can choose one from several operating system options. I chose Ubuntu as it is powerful and, best of all, free.

However, it was not as straight forward as I had expected. There were a bunch of tricky parts. (To be honest, I'm not too familiar with Linux setup. This turned out increasing the difficulties.) And, as a Ubuntu beginner, I realised that I needed to install everything by myself to make it work properly. (Windows, in my early days, didn't train me for this. Sigh..) So, the first step I did was to find out what type of GPU my AWS instance got by typing the following command:

{% highlight linux %}
lpsci -v | less
{% endhighlight %}

This will output several different stuff and one of them is the GPU type on your instances. Next, I headed to NVIDIA website and looked for the correct drivers. After downloading it, then I started installing it. And, that's when the frustration began.

It gave an error message telling me to do something that I didn't understand (isn't that always the case for Linux?). I spent hours to google the solution and every time I successfully overcame one problem, the other immediately emerged. After hours of desperation, I ended up visiting [this marvelous website](http://tleyden.github.io/blog/2014/10/25/cuda-6-dot-5-on-aws-gpu-instance-running-ubuntu-14-dot-04/). 

Despite being posted in 2014, the content is proven to be extremely relevant. I successfully installed the driver and get the GPU working perfectly. The only command that I needed to change was to update the linux kernel. Instead of the version suggested in the post, I used the following command to get the latest kernel source:

{% highlight linux %}
$ sudo apt-get install linux-headers-`uname -r`
{% endhighlight %}

So, head on to [the mentioned website](http://tleyden.github.io/blog/2014/10/25/cuda-6-dot-5-on-aws-gpu-instance-running-ubuntu-14-dot-04/) if you're facing similar situations. Happy configuring your AWS instances!