FROM debian:wheezy
MAINTAINER Antoine Millet <antoine@inaps.org>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get -y -qq --force-yes update \
    && apt-get -y -qq --force-yes install apt-utils adduser python python-pip python-requests \
    && apt-get clean

# Install the last v1 version of radicale to export the storage in the V2 format.
# https://radicale.org/1to2/
RUN pip install -i https://pypi.python.org/simple/ radicale==1.1.6

ADD default_radicale_config.conf /default_radicale_config.conf

RUN mkdir /radicale

ADD launcher.py /
RUN chmod +x /launcher.py

RUN addgroup --quiet --system --gid 1000 radicale
RUN adduser --home /radicale --group --quiet --system --uid 1000 radicale

RUN chown radicale:radicale -R /radicale && chmod 755 -R /radicale

USER radicale

EXPOSE 5232

VOLUME /var/log
VOLUME /radicale

CMD []
ENTRYPOINT ["/launcher.py"]
