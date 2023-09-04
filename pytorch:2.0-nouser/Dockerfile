FROM pytorch/pytorch:2.0.0-cuda11.7-cudnn8-devel

# install essential softwares
RUN if [ -e /etc/apt/sources.list.d/cuda.list ] ; then rm /etc/apt/sources.list.d/cuda.list; fi ; apt update
RUN DEBIAN_FRONTEND=noninteractive TZ=Etc/UTC apt-get -y install tzdata
RUN apt install -y vim zsh git ssh sudo language-pack-en tmux libssl-dev python3-dev libmysqlclient-dev sqlite3 build-essential python3-opencv
RUN update-locale LANG=en_US.UTF-8

RUN python -m pip install --upgrade pip
#RUN python -m pip install setuptools packaging

RUN python -m pip install numpy matplotlib pylint tqdm sentencepiece 
RUN python -m pip install transformers scikit-learn 
RUN python -m pip install seaborn wandb pandas optuna 
RUN python -m pip install scikit-optimize opencv-python opt-einsum 
RUN python -m pip install axial-attention ujson datasets unidecode 
RUN python -m pip install fairscale fire sentencepiece
RUN cd llama && python -m pip install -e .


WORKDIR /workspace
