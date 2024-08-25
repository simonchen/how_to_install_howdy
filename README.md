# how_to_install_howdy
A brief how to setup howdy on Ubuntu or distros

## 为pip安装,设置并进入python虚拟环境 (非必要)
```
python3 -m venv ~/py_envs
source ~/py_envs/bin/activate
```

## 开始安装howdy
```
sudo add-apt-repository ppa:boltgolt/howdy
sudo apt update
sudo apt install howdy
```

## 安装完,手工链接howdy (是个py脚本)
```
sudo ln -s /lib/security/howdy/cli.py /usr/local/bin/howdy
```

## 修改IR摄像头设备名
```sudo howdy config```
打开编辑器CTRL+W搜索device_path
改成 device_path = /dev/video0

## 添加面部模型
```sudo howdy add```

如果报错cv2 not found, 执行下面命令安装opencv-python
```
sudo pip install opencv-python --break-system-packages
sudo pip3 install dlib --break-system-packages
```

## 添加到授权公共配置文件(https://wiki.archlinux.org/title/Howdy)
(https://github.com/boltgolt/howdy/issues/59)

添加到顶部:
```
auth sufficient pam_unix.so try_first_pass likeauth nullok
auth    [success=3 default=ignore]        pam_python.so /lib/security/howdy/pam.py
```
on the empty line between "# pam-auth-update(8) for details." and "# here are the per-package modules (the "Primary" block)". You can use nano (sudo nano /etc/pam.d/common-auth) for this if you didn't know already.

## 修复/usr/lib/security/howdy/pam.py 参考 :
[No way to get Howdy to start authentication at system start with Ubuntu 24.04 #927](https://github.com/boltgolt/howdy/issues/927)
