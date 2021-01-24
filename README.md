Big part of this code is used from [dbolya/yolact](https://github.com/dbolya/yolact)
Colab run method is used from [yolact-with-google-colab](https://www.immersivelimit.com/tutorials/yolact-with-google-colab)

# YOLACT
  - YOLACT is a state of the art, real-time, single shot object segmentation algorithm detailed in these papers:
  [YOLACT: Real-time Instance Segmentation](https://arxiv.org/pdf/1912.06218.pdf)
  [YOLACT++: Better Real-time Instance Segmentation](https://arxiv.org/pdf/1904.02689.pdf)

## Installation and running on Google Colab

### Runtime Setup
    Go to Runtime > Change Runtime Type
    Choose GPU (TPU won't work)

- Install required packets
   ```Shell
   #Cython needs to be installed before pycocotools
   !pip install cython
   !pip install opencv-python pillow pycocotools matplotlib
   ```
- Downgrade torch to accommodate DCNv2
   ```Shell
   !pip install torchvision==0.5.0
   !pip install torch==1.4.0
   ```
- Clone YOLACT from github
    ```Shell
   %cd /content
   # Clone the repo
   !git clone https://github.com/harsul/SiamYolact.git
   ```
- DCNv2
   ```Shell
   # Change to the right directory
   %cd /content/yolact/external/DCNv2
   # Build DCNv2
   !python setup.py build develop
   ```
- Pretrained Weights
    ```Shell
    %cd /content
    # Clone the repo
    !git clone https://github.com/chentinghao/download_google_drive.git
    # Create a new directory for the pre-trained weights
    !mkdir -p /content/yolact/weights
    # Download the file
    !python ./download_google_drive/download_gdrive.py 1ZPu1YR2UzGHQD0o1rEqy-j5bmEm3lbyP ./yolact/weights/yolact_plus_resnet50_54_800000.pth
   ```
- Make Folders for input and output videos and upload mot chellenge video into input_videos folder
   ```Shell
   !mkdir /content/input_videos
   !mkdir /content/output_videos
   ```
## Run on Video 
- Change input and output paths
    ```Shell
   %cd /content
    input_path="/content/input_videos/mot17-11.webm"
    output_path = "/content/output_videos/output.mp4"
    !python ./yolact/eval.py --trained_model=./yolact/weights/yolact_plus_resnet50_54_800000.pth --score_threshold=0.15 --top_k=15 -- video_multiframe=4 --video={input_path}:{output_path}
   ```
