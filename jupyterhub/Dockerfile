FROM jupyterhub/jupyterhub:latest AS base

RUN apt update
RUN apt-get install npm nodejs python3 python3-pip git -y

RUN python3 -m pip install jupyterhub notebook jupyterlab

FROM base AS settings

RUN echo 'root:admin' | chpasswd

WORKDIR /home

RUN git clone https://github.com/jupyterhub/nativeauthenticator.git
WORKDIR /home/nativeauthenticator
RUN pip3 install -e .

FROM settings AS service

RUN mkdir /etc/jupyterhub
RUN mkdir /home/common
RUN chmod -R 777 /home/common

WORKDIR /etc/jupyterhub

COPY ./jupyterhub_config.py .

ENTRYPOINT ["jupyterhub", "-f",  "/etc/jupyterhub/jupyterhub_config.py"]
