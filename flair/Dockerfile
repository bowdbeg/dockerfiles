# FROM pytorch/pytorch:1.2-cuda10.0-cudnn7-devel
#FROM pytorch/pytorch:1.3-cuda10.1-cudnn7-devel
#FROM pytorch/pytorch:1.4-cuda10.1-cudnn7-devel
#FROM pytorch/pytorch:1.5-cuda10.1-cudnn7-devel
FROM pytorch/pytorch:1.7.1-cuda11.0-cudnn8-devel
#FROM pytorch/pytorch:1.8.0-cuda11.1-cudnn8-devel

ENV LOCAL_UID 15083
ENV LOCAL_UNAME makino.15083
ENV PASSWORD 15083
ENV GIT_UNAME bowdbeg
ENV GIT_EMAIL bear.kohei@gmail.com
ENV CUDA cu111
ENV TORCH 1.8.0

# install essential softwares
RUN apt update && apt install -y vim zsh git ssh sudo language-pack-en coinor-cbc
RUN sudo update-locale LANG=en_US.UTF-8

# add user
RUN useradd ${LOCAL_UNAME} --uid ${LOCAL_UID} --create-home && usermod -aG sudo ${LOCAL_UNAME}
RUN ln -s /workspace /home/${LOCAL_UNAME}
RUN echo "${LOCAL_UNAME}:${PASSWORD}" | chpasswd

# change login shell
RUN chsh -s /bin/zsh $LOCAL_UNAME

# set my setting of zsh
RUN git clone https://github.com/bowdbeg/my_setting.git /root/my_setting && cp /root/my_setting/.zshrc /home/${LOCAL_UNAME} && chown ${LOCAL_UNAME}:${LOCAL_UNAME} /home/${LOCAL_UNAME}/.zshrc

# pip install packages
RUN pip install numpy matplotlib pylint optuna tqdm sentencepiece transformers scikit-learn tensorboard spacy scispacy flair black pulp

# config git account
RUN git config --global user.name ${GIT_UNAME} && git config --global user.email ${GIT_EMAIL}

# symbolic link
RUN ln -s /workspace /home/${LOCAL_UNAME}/workspace/

# symboloc link to python
RUN ln -s /opt/conda/bin/python /usr/bin/python

RUN pip install https://s3-us-west-2.amazonaws.com/ai2-s2-scispacy/releases/v0.2.5/en_core_sci_sm-0.2.5.tar.gz

# install optuna
RUN sudo apt update && sudo apt install -y libssl-dev python3-dev libmysqlclient-dev && pip install -U optuna mysqlclient scikit-optimize

EXPOSE 22

USER ${LOCAL_UNAME}
WORKDIR /home/${LOCAL_UNAME}
