FROM postgres:9.6.5

RUN apt-get update && \
  apt-get install -y wget unzip python gcc python-dev && \
  wget https://ftp.postgresql.org/pub/projects/pgFoundry/dbsamples/pagila/pagila/pagila-0.10.1.zip -O /tmp/pagila-0.10.1.zip && \
  unzip /tmp/pagila-0.10.1.zip -d /tmp && \
  wget https://bootstrap.pypa.io/get-pip.py && \
  python get-pip.py && \
  cat /tmp/pagila-0.10.1/pagila-schema.sql | \
  # ERROR:  language "plpgsql" already exists
  grep -v "CREATE PROCEDURAL LANGUAGE plpgsql" > /docker-entrypoint-initdb.d/pagila_init.sql && \
  cat /tmp/pagila-0.10.1/pagila-data.sql >> /docker-entrypoint-initdb.d/pagila_init.sql

RUN pip install pgcli
COPY launch_pgcli.sh launch_pgcli.sh
RUN chmod +x launch_pgcli.sh

ENTRYPOINT ["docker-entrypoint.sh"]

EXPOSE 5432
CMD ["postgres"]
