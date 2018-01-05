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
