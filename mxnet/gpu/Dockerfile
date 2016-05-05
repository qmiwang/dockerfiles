FROM wjy/jupyter-cuda:v1
MAINTAINER Jianyong Wang <wangjianyongscu@gmail.com>
ENV REFRESHED_AT 2016-05-05

############# 
# install the core library
RUN apt-get update && apt-get install -y build-essential git libopenblas-dev libopencv-dev
RUN git clone --recursive https://github.com/dmlc/mxnet/ && cd mxnet && \
    cp make/config.mk . && \
    echo "USE_CUDA=1" >>config.mk && \
    echo "USE_CUDA_PATH=/usr/local/cuda" >>config.mk && \
    echo "USE_CUDNN=1" >>config.mk && \
    echo "USE_BLAS=openblas" >>config.mk && \
    make -j8 ADD_LDFLAGS=-L/usr/local/cuda/lib64/stubs
ENV LD_LIBRARY_PATH /usr/local/cuda/lib64:$LD_LIBRARY_PATH 
#############

# python pakcage
# graphviz ensures the visualization of mx.viz.plot_network in ipython notebook

RUN apt-get install -y python-numpy wget unzip graphviz
ENV PYTHONPATH /mxnet/python

RUN pip install graphviz