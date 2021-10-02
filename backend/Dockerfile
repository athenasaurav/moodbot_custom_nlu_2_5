FROM ubuntu:18.04

# Installing Python 3.7
RUN apt-get update -y
RUN apt-get install software-properties-common -y
RUN add-apt-repository ppa:deadsnakes/ppa -y
RUN apt-get update -y
RUN apt-get install python3 -y
RUN apt-get install curl -y
RUN apt-get install -y git
RUN apt-get install python3-pip -y
# Install Poetry 

RUN curl -sSL https://raw.githubusercontent.com/python-poetry/poetry/master/get-poetry.py | python3

CMD [python3 -m venv .venv]
CMD [source .venv/bin/activate]

CMD [source $HOME/.poetry/env]



# install make
RUN apt-get update -y
RUN apt-get -y install make

WORKDIR /app
COPY . /app
COPY ./data /app/data

RUN cd /app && git clone https://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@github.com/athenasaurav/custom_rasa_2_5.git
RUN cd /app/custom_rasa_2_5 && poetry env info && make install

# install rasa
#RUN make install

# install custom dependencies
RUN pip3 install -U pip
RUN pip3 install typing_extensions
RUN pip3 install pandas
RUN pip3 install LanguageIdentifier
RUN pip3 install langdetect
RUN pip3 install pandas
RUN pip3 install transformers
RUN pip3 install sentencepiece
RUN pip3 install torch torchvision torchaudio

#WORKDIR /app
#COPY . /app
#COPY ./data /app/data

RUN  rasa train

VOLUME /app
VOLUME /app/data
VOLUME /app/models

CMD [ "run","-m","/app/models","--enable-api","--cors","*","--debug", "--auth-token", "thisismysecret"]
