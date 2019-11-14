<!--
Licensed to the Apache Software Foundation (ASF) under one
or more contributor license agreements.  See the NOTICE file
distributed with this work for additional information
regarding copyright ownership.  The ASF licenses this file
to you under the Apache License, Version 2.0 (the
"License"); you may not use this file except in compliance
with the License.  You may obtain a copy of the License at

  http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing,
software distributed under the License is distributed on an
"AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
KIND, either express or implied.  See the License for the
specific language governing permissions and limitations
under the License.
-->

# Getting Started with Superset using Docker

Docker is an easy way to get started with Superset.

## Initializing Database
1.替换debian源
在DOCKFILE里增加     #已增加
RUN sed -i 's/deb.debian.org/mirrors.ustc.edu.cn/g' /etc/apt/sources.list
RUN sed -i 's|security.debian.org/debian-security|mirrors.ustc.edu.cn/debian-security|g' /etc/apt/sources.list
  
2.增加SUPERSET依赖的模块包
在requirements-extra.txt里增加 #已增加
pybigquery==0.4.10
pandas_gbq==0.10.0
gsheetsdb==0.1.9
thrift==0.11.0
mysqlclient==1.4.2
psycopg2-binary==2.7.5
elasticsearch-dbapi==0.1.0
sasl==0.2.1
thrift-sasl==0.3.0

To initialize the database with a user and example charts, dashboards and datasets run:

```bash
docker-compose run -e SUPERSET_LOAD_EXAMPLES=yes --rm superset ./docker-init.sh
```
更新debian源

This may take a minute.

## Normal Operation

To run the container, simply run:

```bash
docker-compose up
```

After several minutes for superset initialization to finish, you can open a browser and view [`http://localhost:8088`](http://localhost:8088) 
to start your journey.

## Developing

While running, the container server will reload on modification of the superset python and javascript source code.
Don't forget to reload the page to take the new frontend into account though.

## Production

It is also possible to run Superset in non-development mode: in the `docker-compose.yml` file remove
the volumes needed for development and change the variable `SUPERSET_ENV` to `production`.

## Resource Constraints

If you are attempting to build on a Mac and it exits with 137 you need to increase your docker resources.
OSX instructions: https://docs.docker.com/docker-for-mac/#advanced (Search for memory)
