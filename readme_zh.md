# 中文安装说明

## 1 初始化系统环境

### 1.1 更换加速源

```root@test-c92:~# bash <(curl -sSL https://gitee.com/SuperManito/LinuxMirrors/raw/main/ChangeMirrors.sh)```

```sudo apt install nodejs npm ffmpeg```

修改npm的源：

```npm config set registry https://registry.npmmirror.com```

```npm config get registry```

如果得到https://registry.npmmirror.com/,则加速源设置成功。

### 1.2 安装所需的软件/组件

```npm install pm2 -g```

```npm install express```

## 2 下载simple-nvr

```git clone https://github.com/ixinshang/simple-nvr.git```

下载较慢，也可以采取其他的方式下载（部分系统可能需要安装git）。

## 3 修改相关参数

```root@test-c92:~# cd simple-nvr/```

### 3.1 修改摄像头参数

```vim cameras.json```，例如：

```
[
    {
        "name": "test",
        "url": "rtsp://lxxxx:xxxxx@1.2.2.2:8554/proxied"
    },
    {
        "name": "test2",
        "url": "rtsp://lxxxx:xxxxx@1.1.1.2:8554/proxied"
    }
]
```



### 3.2 修改存储位置参数

```vim storage.json```，例如：

```
`{
    "rootpath": "/root/simple-nvr/snvr"
}`
```



## 4 运行simpel-nvr

### 4.1 启动录像

```node nvr.js ```

后台录像，默认端口**3001**，可查看参数。

### 4.2 通过浏览器查看录像

```node nvr-browser.js ```

web页面，可以在线查看情况，默认端口**3000**。

## 5 带密码启动(两种方法)

### 5.1 使用node命令启用

```nvr_user=Username nvr_password=Secret  node nvr-browser.js``` # 修改对应的值即可。

### 5.2 使用pm2守护运行

**参见pm2.json中的注释。**

注意，pm2的常用命令

```sudo pm2 startup```

```systemctl enable pm2-root```

```systemctl status pm2-root```

```systemctl start pm2-root```

```pm2 save ```

## 6 未完事宜

### 6.1 ~~mkv在浏览器播放有问题~~

由于某些摄像头的编码为h265，导致无法使用chrome在线播放。将摄像头的编码改为h264后，使用chrome播放正常。

### 6.2 ~~大文件的定时删除~~

根据实际使用情况，修改scripts/delete.sh中的视频需要保留的时间和文件存放位置，借助crontab即可定时清理过期的视频。

### 6.3 时区的调整

不熟悉js,还不知道如何下手。

**致谢:**

感谢[**TomHumphries**](https://github.com/TomHumphries/simple-nvr)!

[toc]