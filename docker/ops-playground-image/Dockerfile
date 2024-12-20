###############################################################################
#  Licensed to the Apache Software Foundation (ASF) under one
#  or more contributor license agreements.  See the NOTICE file
#  distributed with this work for additional information
#  regarding copyright ownership.  The ASF licenses this file
#  to you under the Apache License, Version 2.0 (the
#  "License"); you may not use this file except in compliance
#  with the License.  You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
#  Unless required by applicable law or agreed to in writing, software
#  distributed under the License is distributed on an "AS IS" BASIS,
#  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
#  See the License for the specific language governing permissions and
# limitations under the License.
###############################################################################

###############################################################################
# Build Click Count Job
###############################################################################

FROM maven:3.8-eclipse-temurin-17 AS builder

# Get Click Count job and compile it
COPY ./java/flink-playground-clickcountjob /opt/flink-playground-clickcountjob
COPY settings.xml /usr/share/maven/conf/settings2.xml
WORKDIR /opt/flink-playground-clickcountjob
RUN cat /etc/resolv.conf
RUN wget  https://repo.maven.apache.org/maven2/org/apache/flink/flink-table-api-java/1.13.1/flink-table-api-java-1.13.1.pom
RUN  rm /usr/share/maven/conf/settings.xml && \
     cp /usr/share/maven/conf/settings2.xml /usr/share/maven/conf/settings.xml && \
     mvn clean verify


###############################################################################
# Build Operations Playground Image
###############################################################################

FROM apache/flink:1.16.0-scala_2.12-java11

WORKDIR /opt/flink/bin

# Copy Click Count Job
COPY --from=builder /opt/flink-playground-clickcountjob/target/flink-playground-clickcountjob-*.jar /opt/ClickCountJob.jar
