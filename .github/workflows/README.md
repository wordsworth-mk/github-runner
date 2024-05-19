[TOC]

# NOTICE

如果真想迁回原仓库的话，把里面的

`uses: wordsworth-mk/github-runner/.github/workflows/run.yml@main` 改成原仓库下对应的 yml 路径就可以了

# TIPS

```sh
################################
# redis_pool
################################

sudo systemctl restart redis

redis-cli --raw ping

wget https://github.com/jhao104/proxy_pool/archive/refs/heads/master.zip
unzip master.zip

python -m venv venvdir
source venvdir/bin/activate

pip install -r proxy_tool-master/requirements.txt

# TODO 改掉 settings.py 里的密码

# 启动调度程序
python proxyPool.py schedule

# 启动webApi服务
python proxyPool.py server

```
