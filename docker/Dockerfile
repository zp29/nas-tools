FROM python:3.10-alpine

# 设置环境变量
ENV LANG="C.UTF-8" \
    TZ="Asia/Shanghai" \
    NASTOOL_CONFIG="/config/config.yaml" \
    NASTOOL_AUTO_UPDATE=true \
    NASTOOL_CN_UPDATE=true \
    NASTOOL_VERSION=master \
    PS1="\u@\h:\w \$ " \
    PUID=0 \
    PGID=0 \
    UMASK=000 \
    WORKDIR="/nas-tools"

# 复制所需文件
COPY package_list.txt /tmp/
COPY requirements.txt /tmp/
COPY third_party.txt /tmp/

# 安装基本工具和编译依赖
RUN apk add --no-cache curl bash wget git \
    gcc musl-dev python3-dev libffi-dev openssl-dev jpeg-dev zlib-dev \
    nodejs npm

# 安装package_list.txt中的包
RUN cat /tmp/package_list.txt | xargs apk add --no-cache

# 设置时区
RUN ln -sf /usr/share/zoneinfo/${TZ} /etc/localtime && \
    echo "${TZ}" > /etc/timezone && \
    ln -sf /usr/bin/python3 /usr/bin/python

# 安装rclone和mc
RUN curl https://rclone.org/install.sh | bash && \
    if [ "$(uname -m)" = "x86_64" ]; then ARCH=amd64; elif [ "$(uname -m)" = "aarch64" ]; then ARCH=arm64; fi && \
    curl https://dl.min.io/client/mc/release/linux-${ARCH}/mc --create-dirs -o /usr/bin/mc && \
    chmod +x /usr/bin/mc

# 安装Python依赖
RUN pip install --no-cache-dir --upgrade pip setuptools wheel && \
    pip install --no-cache-dir cython && \
    # 尝试逐个安装依赖包，而不是一次性安装
    python -c "import re; f=open('/tmp/requirements.txt'); reqs=[line.strip() for line in f if not line.startswith('#') and line.strip()]; f.close(); import subprocess; [subprocess.call(['pip', 'install', '--no-cache-dir', req]) for req in reqs]"

# 安装PM2
RUN npm install pm2 -g

# 清理
RUN rm -rf /tmp/* /root/.cache /var/cache/apk/*

# 复制应用代码
COPY . ${WORKDIR}
WORKDIR ${WORKDIR}

# 设置系统参数
RUN mkdir -p /etc/sysctl.d && \
    echo 'fs.inotify.max_user_watches=524288' > /etc/sysctl.d/99-nas-tools.conf && \
    echo 'fs.inotify.max_user_instances=524288' >> /etc/sysctl.d/99-nas-tools.conf

# 安装第三方库
RUN cd ${WORKDIR} && \
    git submodule update --init --recursive && \
    # 确保anitopy可以被导入
    cd ${WORKDIR}/third_party/anitopy && \
    python setup.py install && \
    # 确保其他第三方模块也能被导入
    for dir in $(ls -d ${WORKDIR}/third_party/*/); do \
      if [ -f "${dir}setup.py" ]; then \
        cd ${dir} && python setup.py install; \
      fi \
    done && \
    # 添加third_party到Python路径
    python_ver=$(python3 -V | awk '{print $2}') && \
    echo "${WORKDIR}/third_party" > /usr/local/lib/python${python_ver%.*}/site-packages/third_party.pth

EXPOSE 3000
VOLUME ["/config"]
ENTRYPOINT ["/nas-tools/docker/entrypoint.sh"]