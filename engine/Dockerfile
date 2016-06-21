FROM rails:onbuild
MAINTAINER sebastien.beau@akretion.com
# Replace by your uid
RUN groupadd -g 1000 loco && adduser --uid 1000 --gid 1000 loco
RUN mkdir /usr/src/app/tmp &&\
    chown loco -R /usr/src/app/log /usr/src/app/tmp &&\
    chgrp loco -R /usr/src/app/log /usr/src/app/tmp
USER loco
