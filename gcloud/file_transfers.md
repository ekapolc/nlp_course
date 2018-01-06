## Transferring Files From Your Instance To Your Computer ##
Once you are done with your assignments, zip the files you need. Then, copy the file to your local computer using the gcloud compute copy-file command as shown below. **NOTE: run this command on your local computer**:

```
gcloud compute scp [INSTANCE_NAME]:[REMOTE_FILE_PATH] [LOCAL_FILE_PATH]
```

For example, to copy my files to my desktop I ran:

```
gcloud compute scp instance-2:~/answers.zip ~/Desktop
```
Another (perhaps easier) option is to directly download the zip file from Jupyter. After creating answers.zip, you can download that file directly from Jupyter. To do this, go to Jupyter Notebook and click on the zip file (in this case answers.zip). The file will be downloaded to your local computer. 

You can refer to [this page](https://cloud.google.com/compute/docs/instances/transfer-files "Title") for more details on transferring files to/from Google Cloud.
