FROM jupyter/datascience-notebook
MAINTAINER chapmanbe <brian.chapman@utah.edu>
USER root

RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install tree -y
RUN apt-get install graphviz -y
RUN apt-get install less -y
RUN apt-get install openssh-client -y
# ADD RISE /opt/jupyter/RISE/

# Set default editor to vim
RUN update-alternatives --set editor /usr/bin/vim.basic

USER jovyan

# RUN python /opt/jupyter/RISE/setup.py install
RUN conda update conda -y
RUN conda install mpld3 -y
RUN conda install pip -y
RUN conda install pymysql -y
RUN pip install py-postgresql
RUN pip install pydicom
RUN pip install textblob
RUN conda install gensim -y
RUN pip install ipythonblocks
RUN pip install pydotplus
RUN conda install biopython -y
RUN conda install pytables -y
RUN conda install scikit-image -y
RUN pip install nbstripout
RUN conda install nb_conda -y
# RUN nbstripout --install
# "missing" unix commands less, tree
CMD ["start-notebook.sh"]
