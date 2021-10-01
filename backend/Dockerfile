FROM ubuntu:18.04

# Installing Python 3.7
RUN sudo apt update
RUN sudo apt install software-properties-common
RUN sudo add-apt-repository ppa:deadsnakes/ppa
RUN sudo apt update
RUN sudo apt install python3.7

# Install Poetry 

RUN curl -sSL https://raw.githubusercontent.com/python-poetry/poetry/master/get-poetry.py | python3.7


CMD [source $HOME/.poetry/env]
CMD [git clone https://github.com/athenasaurav/custom_rasa_2_5.git]
CMD [cd custom_rasa_2_5]

# install make
RUN sudo apt-get update
RUN sudo apt-get -y install make

# install rasa
RUN make install

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

WORKDIR /app
COPY . /app
COPY ./data /app/data

RUN  rasa train

VOLUME /app
VOLUME /app/data
VOLUME /app/models

CMD [ "run","-m","/app/models","--enable-api","--cors","*","--debug", "--auth-token", "thisismysecret"]