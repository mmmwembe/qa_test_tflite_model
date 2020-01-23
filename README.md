# Run quality test check on the tflite model
# 

1) Download Tflite Model and label.txt from Google Cloud
```
    mkdir tmp
    gsutil cp gs://tpu-cards-bench-test-bucket/tflite/* tmp
```
2) Place copy of the labels.txt file in the tmp folder

3) Create an images directory in the tmp directory

4) Place test images in tmp/images

5) Call label_image.py with the target tflite model, image and labels txt file

```
    python3 label_image.py \
     --image /tmp/test-bs-50.jpeg \
     --model /tmp/detect.tflite \
     --labels /tmp/card_labels.txt
```

