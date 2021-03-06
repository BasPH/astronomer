#
# Copyright 2018 Astronomer Inc.
#
# Licensed under the Apache License, Version 3.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

FROM astronomerinc/ap-base
LABEL maintainer="Astronomer <humans@astronomer.io>"

ARG BUILD_NUMBER=-1
LABEL io.astronomer.docker.build.number=$BUILD_NUMBER
LABEL io.astronomer.docker.module="default-backend"
LABEL io.astronomer.docker.component="default-backend"

ARG VERSION="v0.0.3"
ENV REPO="github.com/astronomerio/default-backend"
ENV REPO_URL="https://${REPO}"

ENV SERVER_ROOT="/usr/share/nginx/html"

# Install NGINX
RUN apk add --no-cache --virtual .build-deps \
		git \
	&& apk add --no-cache \
		nginx \
	&& git clone \
		-c advice.detachedHead=false \
		--depth 1 \
		--branch ${VERSION} \
		${REPO_URL} ${SERVER_ROOT} \
	&& rm -rf ${SERVER_ROOT}/.git \
	&& mkdir -p /run/nginx \
	&& apk del .build-deps

# Copy NGINX configuration to default location
COPY include/nginx.conf /etc/nginx/nginx.conf

# NGINX is configured to listen on 8080
EXPOSE 8080

# Run NGINX
ENTRYPOINT ["nginx", "-g", "daemon off;"]
