# FROM pytorch/pytorch:1.2-cuda10.0-cudnn7-devel
#FROM pytorch/pytorch:1.3-cuda10.1-cudnn7-devel
FROM pytorch/pytorch:1.4-cuda10.1-cudnn7-devel

ENV LOCAL_UID 15083
ENV LOCAL_UNAME makino.15083
ENV PASSWORD 15083
ENV GIT_UNAME bowdbeg
ENV GIT_EMAIL bear.kohei@gmail.com

# install essential softwares
RUN apt update && apt install -y vim zsh git ssh sudo language-pack-en
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
RUN pip install numpy matplotlib yapf pylint optuna tqdm tensorboardX sentencepiece transformers scikit-learn tensorboard torchtext

# config git account
RUN git config --global user.name ${GIT_UNAME} && git config --global user.email ${GIT_EMAIL}

# symbolic link
RUN ln -s /workspace /home/${LOCAL_UNAME}/workspace/

# setup ssh
RUN apt install -y openssh-server
RUN mkdir -p /var/run/sshd
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd
ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile
RUN ssh-keygen -t rsa -b 4096 -P "" -N ""  -f /etc/ssh/ssh_host_rsa_key -y

EXPOSE 22
CMD echo "$PASSWORD" | sudo -S /usr/sbin/sshd -D

USER ${LOCAL_UNAME}
WORKDIR /home/${LOCAL_UNAME}
