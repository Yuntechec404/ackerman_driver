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

## 修改code 設備名稱
根據上述指令確認設備名稱
開啟檔案 /Home/workspace/src/turn_on_wheeltec_robot/launch/include/base_serial.launch
```xml
  <node pkg="turn_on_wheeltec_robot" type="wheeltec_robot_node" name="wheeltec_robot" output="screen" respawn="false">
    <param name="usart_port_name"    type="string" value="/dev/${你的設備名稱}"/>  
    <param name="serial_baud_rate"   type="int"    value="115200"/>
...
```
## 啟動底盤
```
$ cd ackerman_ws/devel/
$ source setup.bash
$ roslaunch turn_on_wheeltec_robot base_serial.launch
```
# 鍵盤控制
安裝
```
sudo apt-get install ros-noetic-teleop-twist-keyboard
```

啟動鍵盤控制
```
rosrun teleop_twist_keyboard teleop_twist_keyboard.py
```

```
Reading from the keyboard  and Publishing to Twist!
---------------------------
Moving around:
   u    i    o
   j    k    l
   m    ,    .

q/z : increase/decrease max speeds by 10%
w/x : increase/decrease only linear speed by 10%
e/c : increase/decrease only angular speed by 10%
anything else : stop

CTRL-C to quit
```
⚠️ 請按 'z'  decrease max speeds by 10%  將每秒的線速度與角速度降到 0.1~0.3，不然車子會暴衝
