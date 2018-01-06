This part of the guide will walk you through the setup of the VM you created. It is divided into three main parts

1. [IP assignment and firewall setup](ip)
2. [Disk management](disk)
3. [Jupyter configuration](jupyter)

<a name='ip'></a>
# 1. IP assignment and firewall setup

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

<a name='disk'></a>
## Connect to Your Virtual Instance ##
Now that you have created your virtual GCE, you want to be able to connect to it from your computer. The rest of this tutorial goes over how to do that using the command line (Gcloud SDK). The easiest way to connect is using the gcloud compute command below. The tool takes care of authentication for you. On OS X, run:

```
./<DIRECTORY-WHERE-GOOGLE-CLOUD-IS-INSTALLED>/bin/gcloud compute ssh --zone=asia-east1-a <YOUR-INSTANCE-NAME>
```

where <YOUR-INSTANCE-NAME> should be homework4. See [this page](https://cloud.google.com/compute/docs/instances/connecting-to-instance) for more detailed instructions. You are now ready to work on Google Cloud. 

You should be logged in with the same name as your username on your local computer. We have setup the development environment under my user account (ekapolc). To switch user, do

```
sudo su ekapolc
```

You will notice that you are now under my user account.

## Checking your GPU ##

First, let's check your GPU. Do

```
nvidia-smi
```

You should see something like the screen below:

![alt text](https://github.com/ekapolc/cattern/raw/master/common/images/nvidia-smi.png "nvidia-smi.png")

The top table shows the GPUs available. You should see one Telsa K80, called GPU number 0. The bottom table shows the processes that use GPUs. You can verify if things are running properly on the GPU by monitoring nvidia-smi.
