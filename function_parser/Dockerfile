FROM python:3.7.3

RUN touch /etc/inside-container

RUN set -ex && pip3 install --upgrade pip
RUN set -ex && pip3 --no-cache-dir install --upgrade jupyter \
    tree_sitter==0.0.5 \
    requests \
    pyhive \
    tqdm \
    pandas \
    python-arango \
    docopt \
    elasticsearch \
    dpu_utils

RUN mkdir -p /src/vendor
RUN mkdir -p /src/build
RUN cd /src/vendor && git clone https://github.com/tree-sitter/tree-sitter-python.git
RUN cd /src/vendor/tree-sitter-python && git checkout tags/v0.14.0

RUN cd /src/vendor && git clone https://github.com/tree-sitter/tree-sitter-javascript.git
RUN cd /src/vendor/tree-sitter-javascript && git checkout tags/v0.13.10

RUN cd /src/vendor && git clone https://github.com/tree-sitter/tree-sitter-typescript.git
RUN cd /src/vendor/tree-sitter-typescript && git checkout tags/v0.14.0

RUN cd /src/vendor && git clone https://github.com/tree-sitter/tree-sitter-go.git
RUN cd /src/vendor/tree-sitter-go && git checkout tags/v0.13.3

RUN cd /src/vendor && git clone https://github.com/tree-sitter/tree-sitter-ruby.git
RUN cd /src/vendor/tree-sitter-ruby && git checkout tags/v0.13.14

RUN cd /src/vendor && git clone https://github.com/tree-sitter/tree-sitter-java.git
RUN cd /src/vendor/tree-sitter-java && git checkout tags/v0.13.0

RUN cd /src/vendor && git clone https://github.com/tree-sitter/tree-sitter-cpp.git
RUN cd /src/vendor/tree-sitter-cpp && git checkout tags/v0.13.14

RUN cd /src/vendor && git clone https://github.com/tree-sitter/tree-sitter-c-sharp.git
RUN cd /src/vendor/tree-sitter-c-sharp && git checkout tags/v0.13.0

RUN cd /src/vendor && git clone https://github.com/tree-sitter/tree-sitter-php.git
RUN cd /src/vendor/tree-sitter-php && git checkout tags/v0.13.1

COPY script/setup.py /src/function-parser/script/setup.py

RUN cd /src/function-parser/script && python setup.py
WORKDIR /src/function-parser

CMD ["jupyter", "notebook", "--ip=0.0.0.0", "--no-browser", "--allow-root", "--NotebookApp.token=''"]
