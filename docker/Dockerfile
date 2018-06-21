FROM continuumio/anaconda3:5.2.0
MAINTAINER tiagoantao@gmail.com

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update; apt-get install -y emacs vim nano openssh-server lxde vnc4server build-essential zlib1g-dev libgsl0-dev -y unzip tmux screen firefox-esr net-tools xinit xfce4-terminal; apt-get remove -y lxterminal; apt-get clean

RUN conda update --all; conda config --add channels r; conda config --add channels bioconda;conda install -y bwa samtools picard vcftools bedtools angsd bioconductor-edger gatk bayescan hisat2 plink2 stacks r r-vegan r-devtools bioconductor-qvalue stringtie;

RUN mkdir /var/run/sshd; ssh-keygen -A; sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/g' /etc/ssh/sshd_config; echo "root:congen" | chpasswd; echo PasswordAuthentication yes >> /etc/ssh/sshd_config;


RUN mkdir /root/.vnc; echo congen > pass; echo congen >> pass; vncpasswd < pass; rm pass
COPY xstartup /root/.vnc
RUN chmod a+x /root/.vnc/xstartup

#RUN ln -s /bin/tar /bin/gtar
#RUN echo "source('https://bioconductor.org/biocLite.R')\nbiocLite('LEA')\ninstall.packages('RepeatABEL', repos='http://cran.us.r-project.org')\ndevtools::install_github('ngthomas/microhaplot', build_vignettes = TRUE)" > R.inst
#RUN R --no-save < R.inst

RUN mkdir /data
VOLUME /data

EXPOSE 22
EXPOSE 5901

COPY run.sh run.sh
RUN chmod a+x run.sh


CMD ./run.sh
VOLUME /data
