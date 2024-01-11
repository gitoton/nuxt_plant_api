FROM node:20.5

WORKDIR /frontend

ENV LC_ALL=C.UTF-8 LANG=C.UTF-8
ENV TZ Asia/Tokyo

RUN apt-get update && apt-get install -y --no-install-recommends \
  git \
  vim \
  && rm -rf /var/lib/apt/lists/*

RUN yarn install

CMD ["bash"]             