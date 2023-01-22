FROM jupyterhub/jupyterhub AS base

RUN apt update
RUN apt-get install npm nodejs python3 python3-pip git -y

RUN python3 -m pip install jupyterhub notebook jupyterlab

FROM base AS settings

RUN pwd

# RUN npm install -g configurable-http-proxy

WORKDIR /home

RUN git clone https://github.com/jupyterhub/nativeauthenticator.git
WORKDIR /home/nativeauthenticator
RUN pip3 install -e .

FROM settings AS service

RUN mkdir /etc/jupyterhub

WORKDIR /etc/jupyterhub

COPY ./jupyterhub_config.py .

ENTRYPOINT ["jupyterhub", "-f",  "/etc/jupyterhub/jupyterhub_config.py"]
