

FROM python:3.9.3-buster
# FROM julia:buster
#python:3.7

RUN dpkg --add-architecture i386

RUN apt-get update && apt-get upgrade -y

# RUN apt-get install tzdata -y
RUN apt-get install git python-dev curl build-essential vim wget libxml2-dev libxmlsec1-dev -y
RUN apt-get install  pulseaudio libasound-dev portaudio19-dev libportaudio2 libportaudiocpp0 -y
RUN pip install --upgrade pip setuptools
RUN python -m pip install --no-use-pep517  pyroomacoustics
RUN python -m pip install requests numpy scipy Cython pybind11 scipy scikit-learn  nara-wpe sounddevice matplotlib seaborn

#共有
RUN mkdir /works && mkdir -p /works/include
#エラーでどうしようもなくなった時
# COPY include/requirements.txt /works/include
# RUN python -m pip install -r /works/include/requirements.txt


#jupyter
RUN apt-get install jupyter-notebook -y

# nteract
RUN pip install nteract_on_jupyter




#julia
RUN mkdir /Julia
WORKDIR /Julia

RUN wget https://julialang-s3.julialang.org/bin/linux/x64/1.6/julia-1.6.0-linux-x86_64.tar.gz && \
  tar -zxvf julia-1.6.0-linux-x86_64.tar.gz

ENV PATH $PATH:/Julia/julia-1.6.0/bin


COPY include/jupyter_add.jl /works/include
RUN julia /works/include/jupyter_add.jl


WORKDIR /works
EXPOSE 8004