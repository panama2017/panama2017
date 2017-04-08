---
layout:     post
title:      "Recurrent Neural Network Review"
subtitle:   ""
date:       2017-01-23
author:     "Baoxiang Pan"
header-img: "img/home.jpg"
comments: true
---
Recurrent Neural Network(RNN) is beatiful and powerful. This post records some useful resources that helped me during my learning. 

The following link provides rounded outline of RNN: [https://www.zybuluo.com/hanxiaoyang/note/485139](http://www.zybuluo.com/hanxiaoyang/note/485139).
   

Given my understanding, the difficulty of training RNN was first proposed by Sepp Hochreiter in 1991, see [this](http://people.idsia.ch/~juergen/fundamentaldeeplearningproblem.html).
   

Also Sepp's supervisor is an extremely interesting guy, see [his website](http://people.idsia.ch/~juergen/).


The difficulty of training RNN was entitled "Gradient Decay". The basic idea of gradient decay is that the gradient back-propagated would explode or decay exponentially as layers increase.  The problem was also explained by Yoshua Bengio (Yumeng is using Yoshua's algorithm for parameter pre-training in her thesis I think, but pre-training is not as hot as last decade because better net structures were more stressed today, and they pursue better results). For Yoshua's work, please refer to [this](http://www.jmlr.org/proceedings/papers/v28/pascanu13.pdf) and [this](http://www.dsi.unifi.it/~paolo/ps/tnn-94-gradient.pdf). 


Gradient decay problem was solved by implementing a better memory flow mechanism for each recurrent layer. This is kind like the implementation of memory gate in computer RAMS, I think. The new structure is named Long Short Term Memory. The paper was in German and the English version can be found [here](http://web.eecs.utk.edu/~itamar/courses/ECE-692/Bobby_paper1.pdf).

The renaissance of RNN is largely due to the development of natural language processing and video analysis in recent years, examples are google translator,  image explanation, etc.. The basic techniques have been there since the Long Short Term Memory Thesis in 1997. But there are some renovation considering the stronger computing power. 


Also I would highly recommend the book by Goodfellow, which helped me a lot for understanding these fascinating facts.  see the [link](http://www.deeplearningbook.org/).
