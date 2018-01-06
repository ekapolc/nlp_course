## Stopping the VM instance ##

Once you finish using the VM, you can stop the VM. Stopping a VM is equivalent to switching off a computer. The data and the machine will still be available after you turn it back on again. To stop the instance, go to the [compute console](http://console.cloud.google.com/compute/) and select the **VM instances** tab

Select the instance and press the stop button at the top

![alt text](https://github.com/ekapolc/nlp_course/raw/master/gcloud/image/stop_del.png "stop")

You should notice the circle in front of the instance name turning gray after a while.

## Deleting the VM instance ##

To delete the instance, you can press the trash button at the top. You then have to go to the **Disks** page and delete the disks as well. Finally, you will also have to go remove the static IPs requested.
