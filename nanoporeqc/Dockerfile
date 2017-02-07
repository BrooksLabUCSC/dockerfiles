FROM ubuntu:14.04

MAINTAINER Jeltje van Baren, jeltje.van.baren@gmail.com

RUN apt-get update && apt-get install -y \
        zlib1g-dev \
        r-base \
        python-matplotlib \
	python-dev \
	python-pip \
	samtools 

RUN pip install RSeQC

RUN sed 's/pdf(/png(/' /usr/local/lib/python2.7/dist-packages/qcmodule/SAM.py | sed 's/\.pdf/.png/' > SAM.py && \ 
	mv SAM.py /usr/local/lib/python2.7/dist-packages/qcmodule/SAM.py

ADD nanoporeQC	/usr/local/bin/
ADD run_npqc	/usr/local/bin/
ADD samAlignStats.py /usr/local/bin

RUN mkdir /data
WORKDIR /data

ENTRYPOINT ["/bin/bash", "run_npqc"]
CMD ["-h"]

# And clean up
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

