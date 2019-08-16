# Python 以及 Jupyter Notebook

[w3schools](https://www.w3schools.com/python/default.asp)

## 安装 python 以及 工具包

:white_check_mark: Ubuntu 16.04 以上版本预装了Python 3和Python 2。 为确保是最新版本，用 `apt-get` 更新和升级系统：

```sh
$ sudo apt-get update
$ sudo apt-get -y upgrade
```

本地系统到 python 官网下载安装包双击安装。

### 安装 pip

[安装库文件管理工具 pip](https://pip.pypa.io/en/stable/installing/) 

> Windows 中安装完要加到 $path$ 路径变量中去。

远程终端安装

```sh
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
python get-pip.py
pip install -U pip # Upgrading pip
```

安装 pip3

```sh
sudo apt-get -y install python3-pip
```



### 基础工具包

#### 数学包

```sh
# NumPy（Numerical Python的简称）是高性能科学计算和数据分析的基础包。
pip install numpy
# or 
pip install scipy
pip install pandas # 构建在 numpy 之上的数学处理包
# 查看package是否已经安装
pip show scipy
```
#### matplotlib

这个包时负责图形处理。

安装 `pip install matplotlib`

启动时如果要载入这个包，可以加参数 `ipython --pylab`

### ipython 和 jupyter

```sh
pip3 install --upgrade pip
pip3 install jupyter
# 启动 jupyter 
jupyter notebook 
```

启动 `jupyter` 之后， 在网页的右上角新建一个 `.ipynb` 文件，就可以网页版的互动行命令。而直接在终端启动的 `ipython`就是存储的终端，比较难用。这个**jupyter** 其实可以布局到服务器中，那么

#### Ubuntu 服务器 安装 jupyter

```sh
pip install Jupyter # 安装 jupyter 
jupyter notebook --generate-config # 生成Jupyter Notebook配置文件
jupyter notebook password # 配置密码
Enter password: # 我在自己服务器的密码是 
Verify password: 
[NotebookPasswordApp] Wrote hashed password to /root/.jupyter/jupyter_notebook_config.json
```

> 安装过程出现错误：
> ERROR: jsonschema 3.0.2 has requirement six>=1.11.0, but you'll have six 1.10.0 which is incompatible.
>
> 运行安装相应版本额度 six 
>
> `pip install six==1.11.0`

:bell: 因为 **Jupyter notebook** 可以启动终端，并进行任何操作。所以十分危险，密码一定要够健壮。修改密码的命令是 `jupyter notebook password`。



设置服务器配置文件

```python
vim ~/.jupyter/jupyter_notebook_config.py

c.NotebookApp.ip = '*' #所有绑定服务器的IP都能访问，若想只在特定ip访问，输入ip地址即可
c.NotebookApp.port = 8888 #将端口设置为自己喜欢的吧，默认是8888
c.NotebookApp.open_browser = False #我们并不想在服务器上直接打开Jupyter Notebook，所以设置成False
c.NotebookApp.notebook_dir = '/root/jupyter_projects' #这里是设置Jupyter的根目录，若不设置将默认root的根目录，不安全
c.NotebookApp.allow_root = True # 为了安全，Jupyter默认不允许以root权限启动jupyter 
```

最后启动jupyter远程服务器 `jupyter notebook`

> 入门级: `jupyter notebook --allow-root > jupyter.log 2>&1 &`
>
> 进阶版: `nohup jupyter notebook --allow-root > jupyter.log 2>&1 &`
>
> 用`&`让命令后台运行, 并把标准输出写入jupyter.log中
>
> `nohup`表示no hang up, 就是不挂起, 于是这个命令执行后即使终端退出, 也不会停止运行.
>
> 执行上面第2条命令, 可以发现关闭终端重新打开后, 用`jobs`找不到jupyter这个进程了, 于是要用`ps -a`, 可以显示这个进程的pid.  `kill -9 pid` 可以终止进程。



### PyQt

[PyQt4](https://www.lfd.uci.edu/~gohlke/pythonlibs/#pyqt4)  安装相应版本

`pip install PyQt4-4.11.4-cp35-none-win_amd64.whl`

[PyQt5](https://www.riverbankcomputing.com/static/Docs/PyQt5/installation.html)

 `pip install PyQt5`

启动基于 Qt 的控制台 `ipython qtconsole --pylab=inline`


## 语法要点

### jupyter 命令键

> `ESC`   切换到命令模式（命令模式相当于视图模式，不是命令行）
>
> `A`  在当前单元格上方创建一个单元格
> `B`  在当前单元格下方创建一个单元格
> `L`  打开/关闭行号
> `DD` 删除当前单元格
> `S`  手动保存笔记本
> `command`+`shift`+`P` 调出命令行，适用于谷歌个safari
> `H` 查询命令行命令
>
> `Y`    从markdown切换到单元格
> `M`   从单元格却换到markdown
>
> `shift+Enter` 执行命令，打印输出
