# Run quality test check on the tflite model
# 

1) Download Tflite Model and label.txt from Google Cloud
```bash
    mkdir tmp
    gsutil cp gs://tpu-cards-bench-test-bucket/tflite/* tmp
```
2) Place copy of the labels.txt file in the tmp folder

3) Create an images directory in the tmp directory

4) Place test images in tmp/images

5) Upload to Github (if not previously done)


6) In GCP Cloud Shell, setup VM Variables (Note: May have to run step 4 first, as needed)
```bash
    export PROJECT_ID=project-2019-3mega-01
    export ZONE=us-central1-a
    export INSTANCE_NAME=vm-obj-det-tpu-ubuntu
```
7) Start VM
```bash
    gcloud compute instances start $INSTANCE_NAME --zone $ZONE
    gcloud compute instances list
```
8) SSH into VM
```bash
    gcloud compute ssh --project $PROJECT_ID --zone $ZONE $INSTANCE_NAME
```

9) On GCP VM, install tflite intepreter package for the appropriate Python version (e.g 3.5):

```bash

    curl https://dl.google.com/coral/python/tflite_runtime-1.14.0-cp35-cp35m-linux_x86_64.whl --output tflite_runtime-1.14.0-cp35-cp35m-linux_x86_64.whl


    pip3 install tflite_runtime-1.14.0-cp35-cp35m-linux_x86_64.whl
```
10) Clone the QA test Git directory

```bash
    git clone https://github.com/mmmwembe/qa_test_tflite_model.git
```

11) Change directory into the "qa_test_tflite_model" directory

```bash
    cd qa_test_tflite_model
```

12) Run label_image.py with the target tflite model, image and labels txt file

```bash
    python3 label_image.py \
     --image /tmp/images/test-bs-50.jpeg \
     --model_file /tmp/detect.tflite \
     --label_file /tmp/cards_labels.txt
```

