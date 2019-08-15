# Angular 环境

## 开发环境

- Node > 8.9.0
- nom > 5.6.0
- Typescript
- brew

```sh
curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
sudo apt-get install -y nodejs
node --version # v10.16.2
npm -v # 6.9.0
npm install -g typescript # 3.5.3
npm install -g @angular/cli # angular 开发环境
ng --version # 
```

> Angular CLI: 8.2.1
> Node: 10.16.2
>
> OS：linux x64
>
> ------
>
> @angular-devkit/architect       0.802.1
> @angular-devkit/core               8.2.1
> @angular-devkit/schematics   8.2.1
> @schematics/angular               8.2.1
> @schematics/update                0.802.1
> rxjs                                                6.4.0



### Install `watchman`

在 Mac OS 上直接 `$ brew install watchman` 就可以， Ubuntu 上稍微麻烦点， 如下：

```sh
apt-get install -y pkg-config
git clone https://github.com/facebook/watchman.git
cd watchman/
git checkout v4.9.0
sudo apt-get install -y autoconf automake build-essential python-dev libssl-dev libtool
./autogen.sh
./configure
make
sudo make install

watchman --version
```


## 常用命令

### 运行

在 `goormIDE` 上运行服务, [Goorm Quick Tutorial for Development Angular](https://rottk.tistory.com/entry/Goorm-IDE-Quick-Tutorial-for-Development-Angular)

```sh
# 本地机 直接 ng serve 就好了
ng serve --host 0.0.0.0 --port 4200 --disable-host-check
```

### 添加模块

```
ng generate component compnentName
```