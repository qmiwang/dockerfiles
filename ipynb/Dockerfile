FROM kaixhin/mxnet
#FROM kaixhin/theano

ENV REFRESHED_AT 2015-12-08

#RUN apt-get update
#RUN apt-get -y install dialog
RUN apt-get install -y ipython ipython-notebook
RUN apt-get install -y python-pip
RUN pip install --upgrade pip

# plot figures
RUN pip install matplotlib
# another network structure visualization used in theano
# RUN pip install networkx
# dependecy package of mx.viz.plot_network
RUN pip install graphviz
# following command ensures the visualization of mx.viz.plot_network in ipython notebook
RUN apt-get install -y graphviz

EXPOSE 8888

RUN mkdir /research
WORKDIR /research
ADD setup.sh /root/setup.sh
RUN chmod +x /root/setup.sh
#CMD ["ipython", "notebook", "--pylab", "inline", "--ip=0.0.0.0"]
#CMD ln /dev/null /dev/raw1394
#ENTRYPOINT ["ipython", "notebook", "--pylab", "inline", "--ip=0.0.0.0"] 
ENTRYPOINT ["/bin/bash"]