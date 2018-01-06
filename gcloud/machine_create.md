## Creating a GPU Instance ##

After you recieved a confirmation email for the quota increase, you can now start a GPU instance.

Setting up a GPU instance from scratch is time consuming (took me half a day), so we provide you with a VM image that you can use. GCloud does not support publically shared images (yet), but it can be shared to specific people. In order for us to be able to share the image, post your email in the specific discusssion topic on Piazza.

After getting access to the image, use gcloud SDK to create the instance with the command

```
gcloud compute instances create homework --image nlp --image-project august-ensign-168512 --no-boot-disk-auto-delete --machine-type n1-standard-8 --zone asia-east1-a
```

*--image-project* refers to my GCloud account, where you will be grabbing the VM image *nlp* from.

If this completes successfully, you should see an instance in the GCloud web console.

**NOTE: Use your GPUs sparingly because they are expensive. See the pricing [here](https://cloud.google.com/compute/pricing#gpus "title").**

## Setting up the machine ##

The current machine has no gpu in it. We need to do one additional tweak to add a GPU to the instance. To edit the virtual instance, go to the **Compute Engine** menu on the left column of your dashboard (the cloud website) and click on **VM instances**. You should see an instance name **homework
**. Click on the 3 dots next to homework, select **stop** to stop the instance. Stopping the instance shut downs the machine, but you can turn it back on (You will be charged only when the machine is turned on. You can also delete the instance after you are done with the assignment afterwards.) Once the instance is stopped, the green color in front of the instance name should become grey as shown on the picture below.

![alt text](https://github.com/ekapolc/cattern/raw/master/common/images/google-cloud-start-stop-instance.png "google-cloud-start-stop-instance.png")

Click on the instance name (homework) to edit the instance. Here, we will add a gpu and do some additional tweaking. Click on **EDIT** at the top right next to VM instance details. Under **machine type** click **customize**. Select **GPUs**, change the number of **GPUs** to **1** and **GPU type** to **NVIDIA Tesla K80**. Scroll down to Firewalls, click **Allow HTTP traffic** and **Allow HTTPS traffic**.

![alt text](https://github.com/ekapolc/cattern/raw/master/common/images/google-cloud-edit-instance.png "google-cloud-edit-instance.png")

## Adding a data disk ##

The image we provided only have 10GB of disk space. You will need more in order to finish the assignment. 

On the edit instance page, scroll to the **additional disks**. Click **Add item**.

![alt text](https://github.com/ekapolc/cattern/raw/master/common/images/google-cloud-additional-disks.png "google-cloud-additional-disks.png")

Under disk creation, name the new disk, select standard persistent disk, None (blank disk), and 50 GB. Click create, and save the instance edition.

![alt text](https://github.com/ekapolc/cattern/raw/master/common/images/google-cloud-disk-create.png "google-cloud-disk-create.png")

## Connect to Your Virtual Instance ##
Now that you have created your virtual GCE, you want to be able to connect to it from your computer. The rest of this tutorial goes over how to do that using the command line (Gcloud SDK). The easiest way to connect is using the gcloud compute command below. The tool takes care of authentication for you. On OS X, run:

```
./<DIRECTORY-WHERE-GOOGLE-CLOUD-IS-INSTALLED>/bin/gcloud compute ssh --zone=asia-east1-a <YOUR-INSTANCE-NAME>
```

where <YOUR-INSTANCE-NAME> should be homework. See [this page](https://cloud.google.com/compute/docs/instances/connecting-to-instance) for more detailed instructions. You are now ready to work on Google Cloud. 

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


## Formating the data disk and mounting the data disk ##

The disk you just added will be unformatted and not mounted, so we need additional steps in order to use the disk. We follow the guide [here](https://cloud.google.com/compute/docs/disks/add-persistent-disk#formatting). First, start the instance and connect to it.

In the terminal, use the `lsblk` command to list the disks that are attached to your instance and find the disk that you want to format and mount.

![alt text](https://github.com/ekapolc/cattern/raw/master/common/images/google-cloud-disk-list.png "google-cloud-disk-list.png")

In order case, the new disk is `sdb` (notice the size is 50GB). Format the disk by the command (change sdb if necessary).

```
sudo mkfs.ext4 -m 0 -F -E lazy_itable_init=0,lazy_journal_init=0,discard /dev/sdb
```

Make a mounting point. In this case, we name it `data`.

```
sudo mkdir -p /mnt/disks/data
```

Mount sdb onto data, and configure read write permission. Create a symbolic link to mount location.

```
sudo mount -o discard,defaults /dev/sdb /mnt/disks/data
sudo chmod a+w /mnt/disks/data
sudo ln -s /mnt/disks/data /data
```

You can now access the new disk at /data

Finally, we want the OS to remember that we added this disk at this location. We need to edit a system file for this. Use the following commands:

```
sudo cp /etc/fstab /etc/fstab.backup
echo UUID=`sudo blkid -s UUID -o value /dev/sdb` /mnt/disks/disk-1 ext4 discard,defaults,nofail 0 2 | sudo tee -a /etc/fstab
```

# Trouble Shooting #

If you get this error when running nvidia-smi
```
Failed to initialize NVML: Driver/library version mismatch
```
Follow the instructions in [stackoverflow](https://stackoverflow.com/questions/43022843/nvidia-nvml-driver-library-version-mismatch)
