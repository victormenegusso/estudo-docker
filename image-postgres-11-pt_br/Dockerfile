
FROM postgres:11.1

LABEL version="0.0.1"
LABEL name="postgres_pt_br:11.1"
LABEL release-date="2018-11-10"
LABEL description="PostgreSQL 11.1 pt_BR.UTF8"

RUN localedef -i pt_BR -c -f UTF-8 -A /usr/share/locale/locale.alias pt_BR.utf-8

ENV LANG pt_BR.utf8