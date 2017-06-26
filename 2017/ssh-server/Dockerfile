FROM sickp/alpine-sshd
MAINTAINER chapmanbe <brian.chapman@utah.edu>
# for physionet instructions see
# https://www.physionet.org/physiotools/wfdb-linux-quick-start.shtml
# dependencies for spell nbextensions (including spell check) and other requirements


# Create jovyan user with UID=1000 and in the 'users' group
RUN apk add --no-cache bash bash-completion
RUN adduser -D -h /home/jovyan -s /bin/bash -u 1000 jovyan && \
    echo "jovyan:jovyan" | chpasswd && \ 
    passwd -d root && \
    sed -i "s/PermitRootLogin yes/PermitRootLogin no/" /etc/ssh/sshd_config

