**Kolomogrov Arnold Networks**
-------------------------------------

This is a small project to test the new Kolomogrov Arnold Networks based on the 
Kolomogrov Arnold Representation theorem: 
Refer: https://arxiv.org/html/2404.19756v1

In MLPs, the activation functions are on the nodes. But in KANs, they are present
on the edges. Additionally , these activation functions are learnable as opposed to the
fixed activation functions on MLPs. 

The activation functions are denoted using B-splines- called basis-splines. A spline 
is a piecewise polynomial function used to fit a set of points smoothly - imagine 
segments of polynomials added together. B-splines give more local control, i.e., changes 
in a specific local region do not propagate to other regions, thus, are more flexible. The 
coefficients of the b-splines are the learnable parameters and the grid of the spline can
also be updated on the fly if the input data changes tremendously.

NOTE: grid is basically a vector of knots. Knots represent the points where the b-splines 
are evaluated or in simple terms intervals between which each spline is fit. More the number 
of grid points --> more the number of intervals --> more the number of splines --> better 
approximation. However, we need to ensure that there is a balance between bias and variance 
(underfitting vs overfitting).

KANs are found to work better on tasks like regression, PDE solving, Continual Learning, etc.,
when compared to MLPs. They gave more accuracy with smaller networks compared to MLPs and show 
better neural scaling laws than MLPs. However, KANs are still extremely new and tests need to 
be performed on much larger datasets and with better MLP benchmarks to establish generality. 
KANs, are also extremely slow due to the wide learnable function space. But the interpretability 
of KANs could be something that is intriguing. It can provide more idea about how the inputs affect 
the outputs and better visibility into the intermediate layers; something that has been hidden and 
obscure in MLPs. So there is scope. Especially given how quantum computing is on the rise, all 
sub-fields on Deep Learning, including KANs, could see a lot of developments in the coming 
future!

This project is a simple KAN training on the MNIST dataset. I've used the entire train dataset - 
60000 samples - for training, passing 100 samples in each batch. Pykan was used to define the KAN 
model - https://github.com/KindXiaoming/pykan?tab=readme-ov-file.

---------------------------
1. **'MNIST MLP' folder:** Trained using 3 layer MLP with 10 nodes in between.

- **Accuracy: 93.18%**   
- **Training Time: 10 mins**

2. **'pykan train' folder:** Trained using the .train API. Losses aren't very good, but it appears the 
API uses RMSE only which could be bad for classification tasks like MNIST

- **1.17e+01 | test loss: 1.36e+01 | reg: 9.52e+04 : 100%|█| 20/20 [1:08:04<00:00, 204.22s/I]**


2. **'MNIST KAN 5' folder:** Trained using a custom train function with a 3 layer KAN and 5 hidden nodes.
Tested on the entire test data. **Contains the trained model file.**


- **Accuracy: 87.42%**
- **Train Time: around 4 hrs**
 

3. **'MNIST KAN 10' folder:** Trained using a custom train function with 3 layer KAN but 10 hidden nodes 
like the MLP case. Tested on 75% of the test data since RAM was crashing with 100% data. **Contains the 
trained model file.**


- **Accuracy: 93.01%**
- **Train Time: around 7 hrs**

---------------------------

From the results, KAN with a similar structure as MLP takes around 7 hours to train giving a similar accuracy 
of 93%. KAN with 5 hidden nodes gives only 87% with 4 hours training time. 

At least for MNIST, the results are not very great. But again, maybe there are different configurations to 
test here and a better system could give more ideas on this. 








