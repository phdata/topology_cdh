# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
FROM alpine:latest
MAINTAINER Dima Spivak <dima@spivak.ch>

ARG CSD_URL=http://archive.cloudera.com/spark2/csd/SPARK2_ON_YARN-2.1.0.cloudera2.jar
ARG PARCEL_URL=http://archive.cloudera.com/spark2/parcels/2.1.0.cloudera2/SPARK2-2.1.0.cloudera2-1.cdh5.7.0.p0.171658-el6.parcel

ARG CSD_DIRECTORY=/opt/cloudera/csd
ARG PARCEL_REPO_DIRECTORY=/opt/cloudera/parcel-repo

RUN apk --no-cache add tar

RUN mkdir -p ${PARCEL_REPO_DIRECTORY} && \
    wget -P ${PARCEL_REPO_DIRECTORY} ${PARCEL_URL} && \
    PARCEL_NAME=$(basename ${PARCEL_URL}) && \
    cd ${PARCEL_REPO_DIRECTORY} && \
    sha1sum ${PARCEL_NAME} | awk '{ print $1 }' > ${PARCEL_NAME}.sha

VOLUME ${PARCEL_REPO_DIRECTORY}

RUN mkdir -p "${CSD_DIRECTORY}" && \
    CSD_NAME=$(basename ${CSD_URL}) && \
    wget -O "${CSD_DIRECTORY}/${CSD_NAME}" "${CSD_URL}"

VOLUME ${CSD_DIRECTORY}

CMD ["/bin/true"]
