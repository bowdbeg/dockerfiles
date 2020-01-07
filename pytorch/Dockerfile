# FROM pytorch/pytorch:1.2-cuda10.0-cudnn7-devel
FROM pytorch/pytorch:1.3-cuda10.1-cudnn7-devel

ENV LOCAL_UID 15083
ENV LOCAL_UNAME makino.15083
ENV PASSWORD 15083
ENV GIT_UNAME bowdbeg
ENV GIT_EMAIL bear.kohei@gmail.com

EXPOSE 22

# install essential softwares
RUN apt update && apt install -y vim zsh git ssh sudo

# add user
RUN useradd ${LOCAL_UNAME} --uid ${LOCAL_UID} --create-home && usermod -aG sudo ${LOCAL_UNAME}
RUN ln -s /workspace /home/${LOCAL_UNAME}
RUN echo "${LOCAL_UNAME}:${PASSWORD}" | chpasswd

# change login shell
RUN chsh -s /bin/zsh $LOCAL_UNAME

# set my setting of zsh
RUN git clone https://github.com/bowdbeg/my_setting.git /root/my_setting && cp /root/my_setting/.zshrc /home/${LOCAL_UNAME} && chown ${LOCAL_UNAME}:${LOCAL_UNAME} /home/${LOCAL_UNAME}/.zshrc

# pip install packages
RUN pip install numpy matplotlib yapf pylint optuna tqdm tensorboardX sentencepiece transformers scikit-learn tensorboard

# config git account
RUN git config --global user.name ${GIT_UNAME} && git config --global user.email ${GIT_EMAIL}

# symbolic link
RUN ln -s /workspace /home/makino.15083/workspace/

# setup ssh
RUN apt install -y openssh-server sysv-rc-conf
RUN mkdir -p /var/run/sshd
RUN sysv-rc-conf ssh on
#RUN ssh-keygen -t rsa  -N '' -f /etc/ssh/ssh_host_rsa_key && ssh-keygen -t dsa  -N '' -f /etc/ssh/ssh_host_dsa_key
RUN /etc/init.d/ssh start

USER ${LOCAL_UNAME}
WORKDIR /home/${LOCAL_UNAME}
