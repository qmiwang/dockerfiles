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
RUN apt-get install -y python-numpy wget unzip
ENV PYTHONPATH /mxnet/python

# plot figures
RUN pip install matplotlib

# dependecy package of mx.viz.plot_network
RUN pip install graphviz
# following command ensures the visualization of mx.viz.plot_network in ipython notebook
RUN apt-get install -y graphviz

RUN pip install scipy
RUN pip install scikit-image
RUN pip install Flask

# expose 8888 as jupyter's default
EXPOSE 8888
EXPOSE 8787
EXPOSE 7777
EXPOSE 9797

# Set a seperated workspace as working directory
WORKDIR /root/workspace
# Optionally expose the workspace to the host
VOLUME ["/root/workspace"]

# Add Tini.  Tini operates as a process subreaper for jupyter. This prevents kernel crashes.
ENV TINI_VERSION v0.8.4
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /usr/bin/tini
RUN chmod +x /usr/bin/tini

ENTRYPOINT ["/usr/bin/tini", "--"]
# Run notebook for ipython defaultly
CMD ["jupyter", "notebook", "--ip=0.0.0.0", "--port=8888","--no-browser"]
