---
title: "Iterative training using Tensorflow and Tensorpack "
excerpt: "Managing GPU memory and GPU handle is the key point to figure out"
toc: true
toc_sticky: true
published: true
header:
  teaser: /assets/images/2021/01/16/tensorflow_tensorpack_iterative_training.png
  image: /assets/images/2021/01/16/tensorflow_tensorpack_iterative_training.png
  caption: "Photo by me"
  og_image: /assets/images/2021/01/16/tensorflow_tensorpack_iterative_training.png
layout: single
# classes: wide

categories:
    - Deeplearning
tags:
    - Tensorflow
    - Tensorpack
last_modified_at: 2021-01-16T08:06:00-05:00
---

# Intro 
To improve a deep learning model performance, I try to reproduce a research paper; "Naive-Student: Leveraging Semi-Supervised Learning in Video Sequences for Urban Scene Segmentation". [[1]](#first) By using Tensorflow and Tensorpack, I stuck handling iterative training. The iterative training means the below pseudo code. The approach of the paper is utilizing semi-supervised learning and the teacher-student model. In each iteration, a teacher can be replaced by a student optionally. Ok, I need to develop iterative training using Tensorflow and Tensorpack. 

```python
def model_training(): 
  # loading data and building model
  with tf.Session() as sess: 
    sess.run()

ITER = 5
for i in range(ITER):
  model_training()
```

# Environment 
The recent version of Tensorflow is 2.4. I provide my environment since, in this post, I've tried it with the old version of Tensorflow. Tensorpack is a wrapper of Tensorflow. It helps the user focus on building the model. [[4]](#four)
```text
Tensorflow-gpu==1.14
Tensorpack==0.10.0
```

# Manage GPU memory 
We can't use a CPU to train our model because it will take too many hours or even days. We are going to use GPU. We need to take care of managing the GPU memory. The problem is after training by Tensorflow the GPU memory is not released. The clearing of memory occurs after the process is over. According to this thread [[2]](#second), we can solve using a numba package or multiprocessing. 

## Numba package (not working)
```python
cuda.select_device(1)
cuda.close()
```
I tried this approach first since the code is short, easy, and intuitive. As many said in the thread[[2]](#second), It won't work for my case. I found no problem in the first iteration but in the second iteration, it crashes. 

## Multiprocessing (not working, promising)
```python
import multiprocessing

def model_training(): 
  # loading data and building model
  with tf.Session() as sess: 
    sess.run()

ITER = 5
for i in range(ITER):
  p = multiprocessing.Process(target=model_training()
  p.start()
  p.join()
  model_training()
```
Tried this approach, it looks promising when we use only **Tensorflow** but with Tensorpack. It won't back after the start function is calling for my case. It hangs on after the start function. If you are same with me using Tensorpack with Tensorflow, please avoid this approach. 

## Fork (not working)
```python
import multiprocessing

def model_training(): 
  # loading data and building model
  with tf.Session() as sess: 
    sess.run()

ITER = 5
for i in range(ITER):
  child_pid = os.fork()
  if child_pid == 0:
    model_training()
  else: 
    os.wait() 
```
Since the multiprocessing approach is failed, I work around multiprocessing with the lower level which is the "fork". I remembered that it works for clearing the GPU memory if I use it alone. However, in this scenario, it won't. 

## GAN trainer, custom Tensorpack trainer (best way)
If we use Tensorpack, I think the best approach is implementing a custom trainer class by inheriting the TowerTrainer. In fact, we need to implement run_step function. [[3]](#third)
```python
def run_step(self):
  # Define the training iteration
  if self.global_step % (self._d_period) == 0:
  self.hooked_sess.run(self.d_min)
  if self.global_step % (self._g_period) == 0:
  self.hooked_sess.run(self.g_min)
```
The run_step function works like a global for-loop. So, we can bring the iterative training code in here. Or, we can find more references using the keyword "Tensorpack GAN trainer". 

# Outro
In this post, we learned that to train the deep learning model using Tensorflow and Tensoapck, we need to take a look at the custom trainer especially the GAN trainer. Since I've been stuck in this issue for a while, I would like to make a note in my blog. 

# Reference 
<a name="first">[1]</a> [https://arxiv.org/abs/2005.10266](https://arxiv.org/abs/2005.10266)

<a name="second">[2]</a> [https://stackoverflow.com/questions/39758094/clearing-tensorflow-gpu-memory-after-model-execution](https://stackoverflow.com/questions/39758094/clearing-tensorflow-gpu-memory-after-model-execution)

<a name="third">[3]</a> [https://github.com/tensorpack/tensorpack/blob/master/examples/GAN/GAN.py#L187](https://github.com/tensorpack/tensorpack/blob/master/examples/GAN/GAN.py#L187)

<a name="four">[4]</a> [https://tensorpack.readthedocs.io/](https://tensorpack.readthedocs.io/)