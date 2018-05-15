## Creating a GPU Instance ##

After you recieved a confirmation email for the quota increase, you can now start a GPU instance.

Setting up a GPU instance from scratch is time consuming (took me half a day), so we provide you with a VM image that you can use. GCloud does not support publically shared images (yet), but it can be shared to specific people. <del>In order for us to be able to share the image, post your email in the specific discusssion topic on Piazza.</del> The image sharing is now disabled, to get access to the image download from [Gdrive](https://drive.google.com/file/d/1iNw5v7nQvi3zGMj7wg9b8K-_og7JHQzs/view?usp=sharing) and follow the instructions [here](https://cloud.google.com/compute/docs/images/import-existing-image)

After getting access to the image, go to the [compute engine page](https://console.cloud.google.com/compute/). Make sure the top of the page next to Google Cloud Platform shows the correct project name.

Click **VM Instances** and click **create instance**

1. Name your instance
2. Zone select **asia-east-1a**
3. Machine type **4 vCPUs.** click **customize.** Click on **GPUs**, select **1** and **NVIDIA Tesla K80** as shown below

![alt text](https://github.com/ekapolc/nlp_course/raw/master/gcloud/image/create_vm1.png "create_vm1.png")

4. Boot disk click **change.** **Custom images** tab select **Cattern Assignment Central** then **nlp** and click **select**

![alt text](https://github.com/ekapolc/nlp_course/raw/master/gcloud/image/boot_disk.png "boot_disk.png")

5. Select **allow http** and **allow https** for Jupyter notebook connections
6. Click **Management, disks, networking, SSH keys** to expand. Go to the **Disks** tab and **uncheck** the **Delete boot disk when instance is deleted.** Click **Add item.** then **Select...** and **Create disk**. In the create disk tab, select **none (blank disk)** under source type. Set **50** GB as the size. Click **create**

![alt text](https://github.com/ekapolc/nlp_course/raw/master/gcloud/image/create_disk.png "create_disk.png")

You screen should look like below.

![alt text](https://github.com/ekapolc/nlp_course/raw/master/gcloud/image/create_vm2.png "create_vm2.png")

**NOTE: Use your GPUs sparingly because they are expensive. See the pricing [here](https://cloud.google.com/compute/pricing#gpus "title").**

## Connect to Your Virtual Instance ##
Now that you have created your virtual GCE, you want to be able to connect to it from your computer. The rest of this tutorial goes over how to do that using the command line (Gcloud SDK). The easiest way to connect is using the gcloud compute command below. The tool takes care of authentication for you. On OS X, run:

```
./<DIRECTORY-WHERE-GOOGLE-CLOUD-IS-INSTALLED>/bin/gcloud compute ssh --zone=asia-east1-a <YOUR-INSTANCE-NAME>
```

where <YOUR-INSTANCE-NAME> should be homework. Another method is to click the **SSH** button next to the instance name to open a connection via the browser window. See [this page](https://cloud.google.com/compute/docs/instances/connecting-to-instance) for more detailed instructions. You are now ready to work on Google Cloud. 

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

Verify that the disk is mounted properly by

```
ls /data
```
If you see **lost+found** the disk is mounted properly.

Finally, we want the OS to remember that we added this disk at this location. We need to edit a system file for this. Use the following commands:

```
sudo cp /etc/fstab /etc/fstab.backup
echo UUID=`sudo blkid -s UUID -o value /dev/sdb` /mnt/disks/data ext4 discard,defaults,nofail 0 2 | sudo tee -a /etc/fstab
```

# Trouble Shooting #

If you get this error when running nvidia-smi
```
Failed to initialize NVML: Driver/library version mismatch
```
Follow the instructions in [stackoverflow](https://stackoverflow.com/questions/43022843/nvidia-nvml-driver-library-version-mismatch)
