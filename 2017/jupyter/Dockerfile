FROM jupyter/datascience-notebook:11be019e4079
MAINTAINER chapmanbe <brian.chapman@utah.edu>
USER root
# for physionet instructions see
# https://www.physionet.org/physiotools/wfdb-linux-quick-start.shtml
# dependencies for spell nbextensions (including spell check) and other requirements

RUN apt-get update && apt-get upgrade -y && apt-get install -y \
      tree \
      graphviz\ 
      less \
      openssh-client \
      gcc \
      libcurl4-openssl-dev \
      libexpat1-dev \
      libnetcdff5 \
      locales-all \
      libxrender-dev \
      libfontconfig-dev \
      libffi-dev \
      rsync \
      mongodb-clients \
      libmariadb-client-lgpl-dev \
  && rm -rf /var/lib/apt/lists/*


# Install physiosnet software
WORKDIR /opt/wfdb
RUN wget https://www.physionet.org/physiotools/wfdb.tar.gz && \
    tar xvfz wfdb.tar.gz 

WORKDIR /opt/wfdb/wfdb-10.5.24
RUN ./configure && \
    make install 
WORKDIR  /opt 
RUN rm -r /opt/wfdb 

WORKDIR /home/jovyan

# Set default editor to vim
RUN update-alternatives --set editor /usr/bin/vim.basic

USER jovyan

RUN conda install -c damianavila82 rise -y

RUN git clone https://github.com/Calysto/notebook-extensions.git
WORKDIR /home/jovyan/notebook-extensions
RUN jupyter nbextension install calysto --user && \
    jupyter nbextension enable calysto/document-tools/main && \
    jupyter nbextension enable calysto/cell-tools/main && \
    jupyter nbextension enable calysto/spell-check/main && \
    jupyter nbextension enable calysto/publish/main && \
    jupyter nbextension enable calysto/submit/main && \
    jupyter nbextension enable calysto/annotate/main 

RUN conda update conda -y && conda install -y \
    mpld3 \
    pip \
    pymysql \
    postgresql \
    gensim \
    biopython \
    pytables \
    scikit-image \
    pymongo \
    spacy 

RUN conda install -y  -c  https://conda.anaconda.org/simpleitk SimpleITK 
RUN conda install -y  -c conda-forge nbstripout

RUN pip install pydicom \
    textblob \
    ipythonblocks \
    pydotplus \
    nbstripout \
    pycontextnlp \
    radnlp \
    fhirclient \
    pivottablejs \
    girder_client \
    nose \
    pyorient

RUN R -e 'install.packages(c("tidyverse","tidytext","icd","RMySQL","DBI","dbplyr","SuperLearner","caret","tensorflow","ggdendro","tree"), dependencies = TRUE, repos = "https://cran.cnr.berkeley.edu/" )'

WORKDIR /home/jovyan
ADD decart_welcome.ipynb /home/jovyan/work/decart_welcome.ipynb
ADD media /home/jovyan/work/media

# RUN nbstripout --install
CMD ["start-notebook.sh"]
