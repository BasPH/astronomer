#
# Copyright 2016 Astronomer Inc.
#
# Licensed under the Apache License, Version 2.0 (the "License");
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

FROM grafana/grafana:5.0.4
LABEL maintainer="Astronomer <humans@astronomer.io>"

ARG BUILD_NUMBER=-1
LABEL io.astronomer.docker=true
LABEL io.astronomer.docker.build.number=$BUILD_NUMBER

RUN apt-get update && apt-get install -yq gettext-base

COPY include/dashboard.yaml /etc/grafana/provisioning/dashboards/dashboard.yaml
COPY include/airflow-scheduler.json /var/lib/grafana/dashboards/airflow-scheduler.json
COPY include/airflow-containers.json /var/lib/grafana/dashboards/airflow-containers.json
COPY include/datasource.yaml /tmp/datasource.yaml
COPY include/entrypoint /entrypoint

ENTRYPOINT ["/entrypoint"]
