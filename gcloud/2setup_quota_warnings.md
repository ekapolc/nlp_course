# Setting up quota warnings

This part of the guide describe how to have GCloud email you if you are exceeding some usage quota. Usually, GCloud bills you monthly and it is hard to keep track of expenses during the meantime. Sometimes it might be too late once the bill arrive. In GCloud you can setup a monthly quota. If you exceed this quota, GCloud will email you. **This does not automatically terminates you service. It is just a warning email. You still need to take action to stop your instances**

To setup the quota first go to [GCloud Console](https://console.cloud.google.com/). Click on the three bars on the top left and click **Billing**. 

![alt text](https://github.com/ekapolc/nlp_course/raw/master/gcloud/image/billing.png "Billing")

**Make sure you have the correct project selected**. It is the project you created in the previous part. Select **Budget & alerts**

![alt text](https://github.com/ekapolc/nlp_course/raw/master/gcloud/image/budget.png "budget")

Click **create budget** Fill as shown below. Make sure to select ** Include credit as a budget expense **

![alt text](https://github.com/ekapolc/nlp_course/raw/master/gcloud/image/create_budget.png "budget creation")

You're done! Note that **this is a monthly budget. The counts reset every month**

