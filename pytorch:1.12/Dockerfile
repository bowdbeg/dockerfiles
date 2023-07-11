# FROM nvcr.io/nvidia/pytorch:22.09-py3
FROM pytorch/pytorch:1.12.1-cuda11.3-cudnn8-devel
# FROM pytorch/pytorch:1.11.0-cuda11.3-cudnn8-devel

ARG UID 1000

# install essential softwares
RUN if [ -e /etc/apt/sources.list.d/cuda.list ] ; then rm /etc/apt/sources.list.d/cuda.list; fi ; apt update
RUN DEBIAN_FRONTEND=noninteractive TZ=Etc/UTC apt-get -y install tzdata
RUN apt install -y vim zsh git ssh sudo language-pack-en tmux libssl-dev python3-dev libmysqlclient-dev sqlite3 build-essential python3-opencv
RUN update-locale LANG=en_US.UTF-8

RUN python -m pip install --upgrade pip
RUN python -m pip install setuptools packaging

# setup apex
WORKDIR /tmp
RUN git clone https://github.com/NVIDIA/apex && cd apex && python -m pip install -v --disable-pip-version-check --no-cache-dir --global-option="--cpp_ext" --global-option="--cuda_ext" ./

RUN python -m pip install numpy matplotlib pylint tqdm sentencepiece transformers scikit-learn tensorboard spacy scispacy black seaborn wandb pandas pytorch_metric_learning==0.9.81 optuna mysqlclient scikit-optimize opencv-python opt-einsum axial-attention ujson

# install scispaCy
RUN python -m pip install https://s3-us-west-2.amazonaws.com/ai2-s2-scispacy/releases/v0.2.5/en_core_sci_sm-0.2.5.tar.gz

RUN yes | adduser --uid $UID --shell /bin/zsh --disabled-password user -q
RUN ln -s /workspace /home/user/workspace && chown user:user /workspace && chmod 755 /workspace
RUN git clone https://github.com/bowdbeg/my_setting.git /root/my_setting && cp /root/my_setting/.zshrc /home/user/.zshrc && chown user:user /home/user/.zshrc

USER user
WORKDIR /workspace
