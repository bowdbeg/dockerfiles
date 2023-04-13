FROM pytorch/pytorch:2.0.0-cuda11.7-cudnn8-devel

ARG UID 1000

# install essential softwares
RUN if [ -e /etc/apt/sources.list.d/cuda.list ] ; then rm /etc/apt/sources.list.d/cuda.list; fi ; apt update
RUN DEBIAN_FRONTEND=noninteractive TZ=Etc/UTC apt-get -y install tzdata
RUN apt install -y vim zsh git ssh sudo language-pack-en tmux libssl-dev python3-dev libmysqlclient-dev sqlite3 build-essential python3-opencv
RUN update-locale LANG=en_US.UTF-8

RUN python -m pip install --upgrade pip
RUN python -m pip install setuptools packaging

RUN python -m pip install numpy matplotlib pylint tqdm sentencepiece transformers scikit-learn tensorboard black seaborn wandb pandas optuna mysqlclient scikit-optimize opencv-python opt-einsum axial-attention ujson

RUN yes | adduser --uid $UID --shell /bin/zsh --disabled-password user -q
RUN ln -s /workspace /home/user/workspace && chown user:user /workspace && chmod 755 /workspace
RUN git clone https://github.com/bowdbeg/my_setting.git /root/my_setting && cp /root/my_setting/.zshrc /home/user/.zshrc && chown user:user /home/user/.zshrc

USER user
WORKDIR /workspace
