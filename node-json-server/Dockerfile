FROM  node:13.1.0-slim
LABEL maintainer="takahiro.yamaki@example.com"

WORKDIR /resource

RUN npm install -g json-server

CMD ["json-server", "--watch", "db.json", "--host", "0.0.0.0"]

EXPOSE 3000
