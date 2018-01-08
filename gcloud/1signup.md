# Google Cloud Signup Tutorial for NLP
Many parts in this tutorial is modified from Stanford's [CS231n's tutorial](http://cs231n.github.io/gce-tutorial/)

# Create and Configure Your Account

For class project and assignments, we will use Google Compute Engine for developing and testing your implementations. This tutorial lists the necessary steps of working on the assignments using Google Cloud. We expect this tutorial to take about an hour. Don’t get intimidated by the steps, we tried to make the tutorial detailed so that you are less likely to get stuck on a particular step. If you have any questions, ask in Piazza.

This tutorial goes through how to set up your own Google Compute Engine (GCE) instance to work on the assignments. When you sign up for the first time, you also receive $300 credits from Google by default. Please try to use the resources judiciously. 

First, if you don’t have a Google Cloud account already, create one by going to the Google Cloud homepage and clicking on Compute. When you get to the next page, click on the blue TRY IT FREE button. If you are not logged into gmail, you will see a page that looks like the one below. Sign into your gmail account or create a new one if you do not already have an account.

![alt text](https://github.com/ekapolc/cattern/raw/master/common/images/cloud-launching-screen.png "Google account signup")

If you already have a gmail account, it will direct you to a signup page which looks like the following.

![alt text](https://github.com/ekapolc/cattern/raw/master/common/images/cloud-for-free.png "Gcloud signup")

Click the appropriate **yes** or **no** button for the first option, and check **yes** for the latter two options after you have read the required agreements. Press the blue **Agree and continue** button to continue to the next page to enter the requested information (your name, billing address and credit card information). Once you have entered the required information, press the blue **Start my free trial** button. You will be greeted by a page like this: 

![alt text](https://github.com/ekapolc/cattern/raw/master/common/images/cloud-dashboard-screen.png "Gcloud dashboard")

To change the name of your project, click on **Manage project settings** on the **Project info** button and save your changes. 

![alt text](https://github.com/ekapolc/cattern/raw/master/common/images/cloud-instance-dashboard-screen.png "cloud-instance-dashboard-screen")

Then, download the Google Cloud SDK that is appropriate for your platform from [here](https://cloud.google.com/sdk/docs/) and follow their installation instructions. **NOTE: this tutorial assumes that you have performed step #4 on the website which they list as optional**. When prompted, make sure you select asia-east1-a as the time zone.


## Requesting GPU Quota Increase ##
To start an instance with a GPU (for the first time) you first need to request an increase in the number of GPUs you can use. To do this, go to your console, click on the **Computer Engine** button and select the **Quotas** menu. You will see a page that looks like the one below.

![alt text](https://github.com/ekapolc/cattern/raw/master/common/images/google-cloud-quotas-screen-upgrade.png "google-cloud-quotas-screen-upgrade.png")

Click on the upgrade account and finish confirm the process. Before you upgrade the account, your instances will be automatically shutdown if you exceed your 300 free trial credits. However, **after upgrading, you will be automatically charged after you used up your credits**. However, this is necessary in order to get access to GPU instances. After upgrading, your screen should look similar to the one shown below.

![alt text](https://github.com/ekapolc/cattern/raw/master/common/images/google-cloud-quotas-screen.png "google-cloud-quotas-screen.png")

Click on the blue **Request Increase** button. This opens a new tab with many quota information. Select **Google Compute Engine API NVIDIA K80 GPUs (asia-east1 region)**. Then, press on the **EDIT QUOTAS** button above. This will open a tab on the right side. Enter the necessary information as shown below

![alt text](https://github.com/ekapolc/cattern/raw/master/common/images/google-cloud-quotas-screen-step1.png "google-cloud-quotas-screen-step1.png")

Click Next, then enter 1 for the quota number, enter the justification as shown. Submit the Request. 

![alt text](https://github.com/ekapolc/cattern/raw/master/common/images/google-cloud-quotas-screen-step2.png "google-cloud-quotas-screen-step2.png")

Once you have your quota increase you can just use GPUs (without requesting a quota increase). After you submit the form, you should receive an email approving your quota increase shortly after (I received my email within a minute). If you don't receive your approval within a day, please inform the instructor. Once you have received your quota increase, you can start an instance with a GPU.
