# POS Tagging

Open your VM and download the jupyter notebook files and Orchid data.
We also provide basic_ff_embedding.pt as a pretrained word embedding in the resources.zip 

For this demo and homework you will need to install additional libraries, python-crfsuite and keras-contrib.

python-crfsuite - is a python implementation of Conditional Random Fields (CRFs) for labeling sequential data.
(https://python-crfsuite.readthedocs.io/en/latest/)

keras-contrib - is a Keras community contributions official extension repository for the python deep learning library Keras. It contains additional layers, activations, loss functions, optimizers, etc. which are not yet available within Keras itself. All of these additional modules can be used in conjunction with core Keras models and modules.
(https://github.com/keras-team/keras-contrib)

You need to run the commands below to install these two libraries.

```
pip install python-crfsuite
git clone https://www.github.com/keras-team/keras-contrib.git
cd keras-contrib
python setup.py install
cd ..
rm -rf keras-contrib
```

To download materials for this homework, run the commands below in your homework directory

```
wget https://www.dropbox.com/s/tuvrbsby4a5axe0/resources.zip
wget --no-check-certificate https://raw.githubusercontent.com/ekapolc/nlp_course/master/HW4/demo.ipynb
wget --no-check-certificate https://raw.githubusercontent.com/ekapolc/nlp_course/master/HW4/HW4-POS Tagging.ipynb
unzip resources.zip
```

Submit the completed notebook file on MyCourseVille ( 4.5 points total, 0.75 points per 1 TODO)

Submit a screenshot of the closed instance (0.5 points)
