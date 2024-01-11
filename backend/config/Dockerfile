FROM python:3.10

WORKDIR /backend

RUN apt-get update && apt-get install -y --no-install-recommends \
    git \
    vim \
    && rm -rf /var/lib/apt/lists/*

# pipのアップデート
RUN pip install --upgrade pip setuptools wheel

COPY ./requirements.txt /backend/requirements.txt

RUN pip install --no-cache-dir -r requirements.txt

CMD [ "bash" ]
