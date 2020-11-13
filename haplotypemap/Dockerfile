FROM statonlab/tripal3

MAINTAINER Lacey-Anne Sanderson <laceyannesanderson@gmail.com>

EXPOSE 3000

WORKDIR /var/www/html/sites/all

RUN curl -sL https://rpm.nodesource.com/setup_10.x | sudo bash - \
  && sudo yum install nodejs -y \
  && node --version && npm --version

RUN cd libraries \
  && git clone https://github.com/kiranbandi/haplotype-map

RUN cd modules \
  && git clone https://github.com/UofS-Pulse-Binfo/haplotype-map-embed haplotypembed

VOLUME /var/www/html/sites/all/libraries/haplotype-map /var/www/html/sites/all/modules/haplotypembed

EXPOSE 80 5432 3000

ENTRYPOINT ["init.sh"]
