# YOLOv5_Ouster-example
Our goal is to identify persons with an [OS0-128](https://ouster.com/products/scanning-lidar/os0-sensor/) lidar sensor and trigger an alarm when the relative distance between the two people is less than 1.8 meters. Detailed instructions can be found in the blog post **Object Detection and Tracking using Deep Learning and Ouster Python SDK**

## Install
1. Clone repo and install required packages in a [Python>=3.7.0](https://www.python.org/) environment, including [PyTorch>=1.7](https://pytorch.org/get-started/locally/). 
```
git clone https://github.com/fisher-jianyu-shi/yolov5_Ouster-lidar-example 
cd yolov5_Ouster-lidar-example 
pip install -r requirements.txt  
```

2. Install the Ouster Python SDK (more details [here](https://static.ouster.dev/sdk-docs/installation.html))  
```
python3 -m pip install --upgrade pip
```

3. Download the [sample lidar data](https://data.ouster.dev/drive/20048), and save both the PCAP and JSON files in the source directory

## Inference with detect.py
`detect.py` (from original [YOLOv5 repo](https://github.com/ultralytics/yolov5)) runs inference on a variety of sources (images, videos, video streams, webcam, etc.) and saves results to `runs/detect`  
For example, to detect people in an image using the pre-trained YOLOv5s model with a 40% confidence threshold, we simply have to run the following command in a terminal in the source directory:
```
python detect.py --class 0 --weights yolov5s.pt --conf-thres=0.4 --source example_pic.jpeg --view-img 
```

This will automatically save the results in the directory `runs/detect/exp` as an annotated image with a label and the confidence levels of the prediction. 

## Inference with detect_pcap.py
To run inference on lidar data (pcap file) using custom-trained weights, simply run:
```
python detect_pcap.py --class 0 --weights best.pt --conf-thres=0.4 --source Ouster-YOLOv5-sample.pcap --metadata-path Ouster-YOLOv5-sample.json  --view-img
```
To calculate the relative distance between two people:
```
python detect_pcap.py --class 0 --weights best.pt --conf-thres=0.4 --source Ouster-YOLOv5-sample.pcap --metadata-path Ouster-YOLOv5-sample.json  --view-img --social-distance
```
