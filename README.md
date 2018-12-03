# SGD NN modeling and Information Plane visualization


## Request
Design a deep-net that obtains high accuracy predictions for the Fashion MNIST dataset [1]. (There are lots of pre-written architectures that you can use as well). 
Obtain the information plane visualization (See Fig 5 in [2]) of the layers' information paths during SGD optimization for the deep-net designed above.

Refs:

* [1] https://github.com/zalandoresearch/fashion-mnist
* [2] https://arxiv.org/abs/1703.00810

# Final Solution 
So far I leverage the existing [code base](https://github.com/mutual-ai/Information-Bottleneck-for-Deep-Learning) on Github, by 
* tuning the learning rate
* Choosing Relu activation function
* Plotting the Information Plane with number of hidden layer changed: from 1 to 6

fme.ipynb is the final plots. 

I also want to writing more about the approaches I used and the future plan for better solution.

# Approaches
## IDNNs
At the beginning, my first option was to choose to base my solution upon this [IDNNs](https://github.com/ravidziv/IDNNs), because it is able to plot almost the same charts as the [paper](https://arxiv.org/abs/1703.00810) demonstrates. 
So, I wanted to leverage this code by passing all the possible hyper-parameters to this algorithm for tuning and plotting.
Generally the pipe line of this algorithm is:

> 1) Load data -> 2) Train and Test the NN model -> 3) Save model data -> 4) Information collection for plotting -> 5) Plotting

After I improved the following features with this repository, the code works functionally. But, I found a blocking issue which is the Information Collection time: even 8 epochs, this code also needs about 30 minutes to do the infomration processing and plotting (after the model is properly trained and tested). Reason is unknown yet.
* Update the code to be able to load Fashion-MNIST
* Update the layer configuration by specifying the number of layers in the command line argument
* Replace the Adam optimizer with SGD

There are two ways of loading the data to the algorithm. 1) is from the mat file (Matlab data files which are part of the original repository), but they are MNIST flavor 2) is from the original .gz files. My later-on experiments found that no matter whether I load MNIST gz files or Fashion-MNIST gz files. The Information Collection time is always much much longer than by loading the data from mat files.

At this time point, more than half of my 24-hour assignment time is gone. So I had to choose some other options.

## Information-Bottleneck-for-Deep-Learning
The coding style is much better in this code repository, which saved some of my time in understanding the code. So I chose to try some luck in there, but the finally charts plotted doesn't have the same style as the paper mentioned. It is a pity.
I also observed another issue: which is with SGD. Within the limited iteration number, using SGD (batch_size is 1)has less acuracy than mini-batch. So I finally choose mini batch (batch_size = 20) and with other tuned hyper-parameters. Perhaps, the hyper-parameters are not properly tuned. But my time was almost up.

# Future Improvements
Because of the time limitation, so far whatever I can submit is the codes or notebooks under this repository. But during the exploration, I think the best way is to 
1) Build the NN model over Tensorflow, train it and test
2) Find a way to be able to save the data for later-on plotting
3) Borrow the plotting code from [IDNNs](https://github.com/ravidziv/IDNNs) to do the plotting, because it's charts is very similar as what the paper shows.

So, the hardest part is how to connect 2) and 3) together. I do want to do such investigation. If you also want to see my result, pls. let me know what is your expected timeline. No matter what, I believe that will be very interesting.

Thank you!  
