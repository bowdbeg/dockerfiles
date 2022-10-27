FROM pytorch/pytorch:1.12.1-cuda11.3-cudnn8-devel
# FROM pytorch/pytorch:1.11.0-cuda11.3-cudnn8-devel

# install essential softwares
RUN if [ -e /etc/apt/sources.list.d/cuda.list ] ; then rm /etc/apt/sources.list.d/cuda.list; fi && apt update && apt install -y vim zsh git ssh sudo language-pack-en tmux libssl-dev python3-dev libmysqlclient-dev sqlite3 build-essential
RUN update-locale LANG=en_US.UTF-8

# python -m pip install packages
RUN python -m pip install --upgrade pip
RUN python -m pip install setuptools packaging

RUN python -m pip install numpy matplotlib pylint tqdm sentencepiece transformers scikit-learn tensorboard spacy scispacy black seaborn wandb pandas pytorch_metric_learning==0.9.81 optuna mysqlclient scikit-optimize
RUN python -m pip install https://s3-us-west-2.amazonaws.com/ai2-s2-scispacy/releases/v0.2.5/en_core_sci_sm-0.2.5.tar.gz

RUN touch /.netrc && chmod 777 /.netrc
RUN mkdir /.config && chmod 777 /.config

WORKDIR /workspace