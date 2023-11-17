FROM pytorch/pytorch:2.1.0-cuda12.1-cudnn8-devel

# install essential softwares
RUN if [ -e /etc/apt/sources.list.d/cuda.list ] ; then rm /etc/apt/sources.list.d/cuda.list; fi ; apt update
RUN DEBIAN_FRONTEND=noninteractive TZ=Etc/UTC apt-get -y install tzdata
RUN apt install -y libssl-dev
RUN apt install -y python3-dev
RUN apt install -y libmysqlclient-dev
RUN apt install -y sqlite3
RUN apt install -y build-essential

RUN python -m pip install --upgrade pip

RUN python -m pip install numpy
RUN python -m pip install --upgrade matplotlib
RUN python -m pip install --upgrade pylint
RUN python -m pip install --upgrade tqdm
RUN python -m pip install --upgrade sentencepiece 
RUN python -m pip install --upgrade transformers
RUN python -m pip install --upgrade scikit-learn 
RUN python -m pip install --upgrade seaborn
RUN python -m pip install --upgrade wandb
RUN python -m pip install --upgrade pandas
RUN python -m pip install --upgrade optuna 
RUN python -m pip install --upgrade scikit-optimize
RUN python -m pip install --upgrade opt-einsum 
RUN python -m pip install --upgrade axial-attention
RUN python -m pip install --upgrade ujson
RUN python -m pip install --upgrade datasets
RUN python -m pip install --upgrade unidecode 
RUN python -m pip install --upgrade fairscale
RUN python -m pip install --upgrade fire
RUN python -m pip install --upgrade sentencepiece
RUN python -m pip install --upgrade accelerate
RUN python -m pip install --upgrade evaluate
RUN python -m pip install --upgrade datasets
RUN python -m pip install --upgrade openicl
RUN python -m pip install --upgrade peft
RUN python -m pip install --upgrade jiwer
RUN python -m pip install --upgrade transformers
Run python -m pip install --upgrade deepspeed
Run python -m pip install --upgrade transformers

# for devel
RUN apt update && apt install -y git

WORKDIR /workspace
