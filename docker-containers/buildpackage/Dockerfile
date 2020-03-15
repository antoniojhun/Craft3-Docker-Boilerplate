FROM node:13

RUN apt-get update && apt-get install -y apt-transport-https \
    && curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
    && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
    && apt-get update \
    && apt-get install -y yarn

WORKDIR /project

COPY ./docker-containers/buildpackage/package.json package.json

COPY ./docker-containers/buildpackage/.eslintrc .eslintrc

RUN cd /project && yarn install

COPY ./docker-containers/buildpackage/gulpfile.js gulpfile.js

CMD ./node_modules/.bin/gulp build