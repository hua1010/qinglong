FROM qinglong_base:latest

RUN git config --global user.email "qinglong@@users.noreply.github.com" \
    && git config --global user.name "qinglong" \
    && git config --global http.postBuffer 524288000 \
    && git clone -b develop https://github.com/hua1010/qinglong.git /ql \
    && npm install -g pnpm \
    && pnpm add -g pm2 ts-node typescript tslib @types/node \
    && pnpm install --prod \
    && cd /ql \
    && cp -f .env.example .env \
    && chmod 777 /ql/shell/*.sh \
    && chmod 777 /ql/docker-pi/*.sh  && dos2unix /ql/docker-pi/*.sh

RUN rm -rf /root/.pnpm-store \
    && rm -rf /root/.local/share/pnpm/store \
    && rm -rf /root/.cache \
    && rm -rf /root/.npm \
    && git clone -b v2.14.7 https://github.com/whyour/qinglong-static.git /static \
    && mkdir -p /ql/static \
    && cp -rf /static/* /ql/static \
    && rm -rf /static \
    && apt-get --purge remove -y gcc make python3-dev default-libmysqlclient-dev libxml2-dev && \
    rm -rf /root/.cache/* && apt-get clean && apt-get autoremove -y
    
ENTRYPOINT ["./docker-pi/docker-entrypoint.sh"]

#docker build -f Dockerfile -t qinglong:latest .
