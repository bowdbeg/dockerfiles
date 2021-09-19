# FROM pytorch/pytorch:1.2-cuda10.0-cudnn7-devel
#FROM pytorch/pytorch:1.3-cuda10.1-cudnn7-devel
#FROM pytorch/pytorch:1.4-cuda10.1-cudnn7-devel
FROM pytorch/pytorch:1.5-cuda10.1-cudnn7-devel

# ENV LOCAL_UID 15083
# ENV LOCAL_UNAME makino.15083
# ENV PASSWORD 15083
ENV GIT_UNAME bowdbeg
ENV GIT_EMAIL bear.kohei@gmail.com

# install essential softwares
RUN apt update && apt install -y vim zsh git ssh sudo language-pack-en
RUN sudo update-locale LANG=en_US.UTF-8

# add user
# RUN useradd ${LOCAL_UNAME} --uid ${LOCAL_UID} --create-home && usermod -aG sudo ${LOCAL_UNAME}
# RUN ln -s /workspace /home/${LOCAL_UNAME}
# RUN echo "${LOCAL_UNAME}:${PASSWORD}" | chpasswd

# change login shell
#RUN chsh -s /bin/zsh $LOCAL_UNAME
RUN chsh -s /bin/zsh

# set my setting of zsh
# RUN git clone https://github.com/bowdbeg/my_setting.git /root/my_setting && cp /root/my_setting/.zshrc /home/${LOCAL_UNAME} && chown ${LOCAL_UNAME}:${LOCAL_UNAME} /home/${LOCAL_UNAME}/.zshrc
RUN git clone https://github.com/bowdbeg/my_setting.git /root/my_setting && cp /root/my_setting/.zshrc /root

# pip install packages
RUN pip install numpy matplotlib yapf pylint optuna tqdm tensorboardX sentencepiece transformers scikit-learn tensorboard torchtext gensim spacy scispacy

# config git account
RUN git config --global user.name ${GIT_UNAME} && git config --global user.email ${GIT_EMAIL}

# symbolic link
# RUN ln -s /workspace /home/${LOCAL_UNAME}/workspace/

# symboloc link to python
RUN ln -s /opt/conda/bin/python /usr/bin/python

# setup apex
# RUN cd /root && git clone https://github.com/NVIDIA/apex.git && cd apex &&  pip install -v --no-cache-dir --global-option="--cpp_ext" --global-option="--cuda_ext" ./

RUN pip install wordcloud pyLDAvis networkx

EXPOSE 22

USER ${LOCAL_UNAME}
WORKDIR /home/${LOCAL_UNAME}

# config git account
# RUN git config --global user.name ${GIT_UNAME} && git config --global user.email ${GIT_EMAIL}

# CMD echo "$PASSWORD" | sudo -S /usr/sbin/sshd -D
