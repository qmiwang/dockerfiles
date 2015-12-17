#mxnet_jupyter
cuda_mxnet:6.5 integrated with ipython jupyter notebook

#Features
#How to use
sudo docker run -d --name neural-style-ipnb1 -v #you workspace#:/root/workspace -p 8888:8888 --device /dev/nvidiactl --device /dev/nvidia-uvm --device /dev/nvidia1 wangjianyong/mxnet_jupyter
