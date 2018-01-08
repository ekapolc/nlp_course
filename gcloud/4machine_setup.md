This part of the guide will walk you through the setup of the VM you created. It is divided into two main parts

1. [IP assignment and firewall setup](#ip-assignment-and-firewall-setup)
2. [Jupyter configuration](#jupyter-configuration)

# IP assignment and firewall setup

### Getting a Static IP Address ###
In order to easily access the VM, we want to assign a fixed IP address to the machine. Note that Google will also charge a very small amount of money to the static IP, so be sure to close it after the course is done.

Change the Extenal IP address of your GCE instance to be static (see screenshot below). 

![alt text](https://github.com/ekapolc/cattern/raw/master/common/images/cloud-external-ip.png "cloud-external-ip.png")

To Do this, click on the 3 line icon next to the **Google Cloud Platform** button on the top left corner of your screen, go to **Networking** and **External IP addresses** (see screenshot below).

![alt text](https://github.com/ekapolc/cattern/raw/master/common/images/cloud-networking-external-ip.png "cloud-networking-external-ip.png")

To have a static IP address, change **Type** from **Ephemeral** to **Static**. Enter your preffered name for your static IP, mine is assignment-1 (see screenshot below). And click on Reserve. Remember to release the static IP address when you are done because according to [this page](https://jeffdelaney.me/blog/running-jupyter-notebook-google-cloud-platform/) Google charges a small fee for unused static IPs. **Type** should now be set to **Static**. 

![alt text](https://github.com/ekapolc/cattern/raw/master/common/images/cloud-networking-external-ip-naming.png "cloud-networking-external-ip-naming.png")

Take note of your Static IP address (circled on the screenshot below). I used 104.196.224.11 for this tutorial.


![alt text](https://github.com/ekapolc/cattern/raw/master/common/images/cloud-networking-external-ip-address.png "cloud-networking-external-ip-address.png")

### Adding a Firewall rule for Jupyter ###
You have to add new firewall rule allowing TCP acess to a particular \<PORT-NUMBER\>. This is used for Jupyter. I usually use 7000 or 8000 for \<PORT-NUMBER\>. Click on the 3 line icon at the top of the page next to **Google Cloud Platform**. On the menu that pops up on the left column, go to **Networking** and **Firewall rules** (see the screenshot below). 

![alt text](https://github.com/ekapolc/cattern/raw/master/common/images/cloud-networking-firewall-rule.png "cloud-networking-firewall-rule.png")

Click on the blue **CREATE FIREWALL RULE** button. Enter whatever name you want: I used assignment1-rules. Enter 0.0.0.0/0 for **Source IP ranges** and tcp:\<PORT-NUMBER\> for **Allowed protocols and ports** where \<PORT-NUMBER\> is the number you used above. Click on the blue **Create** button. See the screen shot below.

![alt text](https://github.com/ekapolc/cattern/raw/master/common/images/cloud-networking-firewall-rule-create.png "cloud-networking-firewall-rule-create.png")

**NOTE:** Some people are seeing a different screen where instead of **Allowed protocols and ports** there is a field titled **Specified protocols and ports**. You should enter tcp:\<PORT-NUMBER\> for this field if this is the page you see. Also, if you see a field titled **Targets** select **All instances in the network**.

### Adding a Firewall rule for Tensorboard ###

Add another firewall rule for Tensorboard (we will use this later in the class). This can be done by repeating the above process for port **tcp:6006**

# Jupyter configuration

### Configuring Jupyter Notebook ###
The following instructions are excerpts from [this page](https://haroldsoh.com/2016/04/28/set-up-anaconda-ipython-tensorflow-julia-on-a-google-compute-engine-vm/) that has more detailed instructions.

The Jupyter configuration file `jupyter_notebook_config.py` is the default config file, jupyter uses when starting. We will create one by (assuming you are login as ekapolc and already activate the virtualenv)

```
rm ~/.jupyter/jupyter_notebook_config.py
jupyter notebook --generate-config
```

Using your favorite editor (vim, emacs etc...) add the following lines to the config file, (e.g.: /home/ekapolc/.jupyter/jupyter_notebook_config.py):

```
c = get_config()

c.NotebookApp.ip = '*'

c.NotebookApp.open_browser = False

c.NotebookApp.port = <PORT-NUMBER>
```

Where \<PORT-NUMBER\> is the same number you used in the prior section (not 6006). Save your changes and close the file. 

### Securing your Jupyter Notebook server ###

In this section, we will add a password to your Jupyter Notebook server (otherwise anyone that knows the ip and port can access your Jupyter server and do nasty things to it).

We start by setting up a password. Do this running a simple script we provide. You will be asked for a password twice, then it will generate a hashed verion of your password.
```
wget --no-check-certificate https://raw.githubusercontent.com/ekapolc/cattern/master/TUMKUD/mkpassword.py
python mkpassword.py
```
Take note of the output (sha1:XXXXXXXXXXX). 

Update `jupyter_notebook_config.py` with
```
c.NotebookApp.password = 'sha1:XXXXXXXXXXX
```

Even if we require a password to login, someone can still get access to our password if our connection is non-encrypted. You can start the notebook to communicate via a secure protocol mode by setting the certfile option to a self-signed certificate which can be easily created by

```
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout mykey.key -out mycert.pem
```

You will be asked with many prompts, but you can keep hitting Enter until it is done.

Then move your cert and key to .jupyter

```
mv mykey.key ~/.jupyter/
mv mycert.pem ~/.jupyter/
```

Update your `jupyter_notebook_config.py` with

```
c.NotebookApp.keyfile = '/home/ekapolc/.jupyter/mykey.key'
c.NotebookApp.certfile = '/home/ekapolc/.jupyter/mycert.pem'
```

Now you are done with the setup and ready to access your Notebook

### Launching and connecting to Jupyter Notebook ###
The instructions below assume that you have SSH'd into your GCE instance using the prior instructions, and have successfully configured Jupyter Notebook.

If you haven't already done so, activate your virtualenv by running:

```
source .env/bin/activate
```

Launch Jupyter notebook using:

```
jupyter-notebook --no-browser --port=<PORT-NUMBER> 
```

Where \<PORT-NUMBER\> is what you wrote in the prior section.

On your local browser, if you go to https://\<YOUR-EXTERNAL-IP-ADDRESS>:\<PORT-NUMBER\>, you will be asked for a password, and then you should see something like the screen below. My value for \<YOUR-EXTERNAL-IP-ADDRESS\> was 104.196.224.11 as mentioned above. You should now be able to start working on your assignments.

![alt text](https://github.com/ekapolc/cattern/raw/master/common/images/jupyter-screen.png "jupyter-screen.png")

If you do not see this, there are several pitfalls.

1. Not using https when connecting.
2. If your key and cert files are mis-configured, the Jupyter page will fail to load. Double check that you points to the correct files.
