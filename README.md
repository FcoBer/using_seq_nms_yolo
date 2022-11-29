# Seq_nms_YOLO

#### Membres: Yunyun SUN, Yutong YAN, Sixiang XU, Heng ZHANG

---

## Introduction


This GitHub provides the instructions to use the project([reference](https://github.com/melodiepupu/seq_nms_yolo.git)) that combines **YOLOv2**([reference](https://arxiv.org/abs/1506.02640)) and **seq-nms**([reference](https://arxiv.org/abs/1602.08465)) for video object detection.

## Instructions

1. Clone the repository to the desired path:
```
git clone https://github.com/FcoBer/using_seq_nms_yolo.git
```
2. Access into the project: 
```
cd using_seq_nms_yolo
```
3. Make your project (this step will return some warnings):
```
make  
```
4. Download the weights of the Network `yolo.weights` and `tiny-yolo.weights`:
```
wget https://pjreddie.com/media/files/yolo.weights
```
```
wget https://pjreddie.com/media/files/yolov2-tiny.weights
```
5. Create the conda environment: 
```
conda create -y -p ./env python=2.7
```
6. Initialize conda environment:
```
conda init
```
7. Close and open the terminal with the same path.
8. Activate the environment:
```
conda activate ./env
```
9. Install the packages:
```
pip install --upgrade tensorflow tf_object_detection
conda install -y opencv matplotlib pillow scipy
```
10. Configure the `PKG_CONFIG_PATH` variable to search in /env/lib/pkgconfig path:
```
PKG_CONFIG_PATH=$PKG_CONFIG_PATH:$(pwd)/env/lib/pkgconfig
export PKG_CONFIG_PATH
```
11. Copy libdarknet and link it with the environment:
```
cp libdarknet.so ./env/lib
cp libdarknet.a ./env/lib
```

12. Access to the video folder.
```
cd video
```

13. Extract the frames of the video (for example: v_ApplyEyeMakeup_g19_c03.avi, you can use other video):
```
python video2img.py -i v_ApplyEyeMakeup_g19_c03.avi
python get_pkllist.py
```

14. Go to the root path:
```
cd ..
```
15. Process the images (the results are in `video/output`):
```
python yolo_seqnms.py
```
16. Make the video with the Yolo algorithm applyied (the video result is in `video`):
```
cd video
```
```
python img2video.py -i output
```
17. If you want to use only Yolo, you can repeat the process from step 12 to 14. In the 15 you have to use:
```
python yolo_without_seqnms.py
```
## Reference

This project copies lots of code from [darknet](https://github.com/pjreddie/darknet) , [Seq-NMS](https://github.com/lrghust/Seq-NMS) and  [models](https://github.com/tensorflow/models).
