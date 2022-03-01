FROM ubuntu

ENV WORKSPACE=/workspace

RUN mkdir $WORKSPACE
WORKDIR $WORKSPACE

RUN apt update && apt install -y git maven tzdata curl
RUN DEBIAN_FRONTEND=noninteractive

# CAEVO
RUN git clone https://github.com/nchambers/caevo.git
WORKDIR $WORKSPACE/caevo
RUN bash getwordnet.sh && echo 'export JWNL=/root/wordnet3.1/jwnl_file_properties.xml' >> ~/.bashrc && source ~/.bashrc && mvn compile
