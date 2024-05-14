# ROS Noetic ackerman_ws
在 ubuntu20.04下使用
## 檢查設備名稱
```
$ cd /dev/
/dev$ ls | grep ttyU
```

OUTPUT：ttyUSB0

## Serial port setting
```
$ sudo chmod 777 /dev/ttyUSB0
```

## 查看設備權限
```
$ ls -all /dev
```
## 建立工作區
```
mkdir -p ackerman_ws
cd ackerman_ws
```

## 下載
```
git clone https://github.com/Yuntechec404/ackerman_driver.git src
```
## 編譯
```
catkin_make
```
## 環境變數
將環境變數新增至.bashrc，下次開啟將自動設定
```
echo "source ~/ackerman_ws/devel/setup.bash" >> ~/.bashrc
```
.bashrc 重啟
```
source ~/.bashrc
```


