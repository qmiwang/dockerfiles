FROM kaixhin/mxnet
#FROM kaixhin/cuda-mxnet:6.5

ENV REFRESHED_AT 2015-12-17

RUN apt-get update && apt-get install -y python-pip
RUN pip install --upgrade pip

# install ipython
# install jupyter
RUN pip install ipython jupyter

# plot figures
RUN pip install matplotlib

# dependecy package of mx.viz.plot_network
RUN pip install graphviz
# following command ensures the visualization of mx.viz.plot_network in ipython notebook
RUN apt-get install -y graphviz

#image processing
RUN pip install scipy
RUN pip install -U scikit-image

# expose 8888 as jupyter's default
EXPOSE 8888

# Set a seperated workspace as working directory
WORKDIR /root/workspace
# Optionally expose the workspace to the host
VOLUME ["/root/workspace"]

# Run ipython defaultly
ENTRYPOINT ["jupyter"]
# Run notebook for ipython defaultly
CMD ["notebook", "--ip=0.0.0.0", "--port=8888","--no-browser"]
