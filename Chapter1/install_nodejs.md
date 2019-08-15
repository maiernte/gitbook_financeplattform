# Node 配置

## 安装 Node 

Mac 或者 Windows 用户， 只要是本地操作，直接到 [官网](https://nodejs.org/en/) 下载 10.16.2 版本，安装。

远程安装根据[安装指南](https://github.com/nodesource/distributions/blob/master/README.md)，选择服务器对应的版本。

**Node.js v10.x**:

```sh
# Using Ubuntu
curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
sudo apt-get install -y nodejs
```

## Node 版本控制

安装 `nvm` 命令行工具。

To **install** or **update** nvm, you can use the [install script](https://github.com/nvm-sh/nvm/blob/v0.34.0/install.sh) using cURL:

```sh
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash
```

or Wget:

```sh
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash
```

安装完成后要执行一次以下命令，并重启终端。

```sh
command -v nvm
```

## yarn 工具包

```sh
sudo apt-get update && sudo apt-get install --no-install-recommends yarn
yarn --version
# 0.31.0
```

如果在安装其它工具包的时候，发现yarn版本不对，执行以下命令，更新yarn的版本

```sh
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
sudo apt update
sudo apt install yarn
```

