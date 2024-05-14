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
crwxrwxrwx   1 root dialout 188,     0 May 14 13:21 ttyUSB0

c:一個字符設備。
rwxrwxrwx:前三個字元表示擁有者的權限，中間三個字元表示所屬群組的權限，最後三個字元表示其他使用者的權限。每組權限都是rwx，意味著所有者、所屬群組和其他使用者都具有讀取、寫入和執行（如果是可執行檔案）的權限。
## 建立工作區
```
mkdir -p ackerman_ws
cd ackerman_ws
```

## 下載
```
/ackerman_ws$ git clone https://github.com/Yuntechec404/ackerman_driver.git src
```
## 編譯
```
/ackerman_ws$ catkin_make
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
1.根據上述指令確認設備名稱

2.開啟路徑檔案 /Home/workspace/src/turn_on_wheeltec_robot/launch/include/base_serial.launch
```xml
  <node pkg="turn_on_wheeltec_robot" type="wheeltec_robot_node" name="wheeltec_robot" output="screen" respawn="false">
    <param name="usart_port_name"    type="string" value="/dev/${你的設備名稱}"/>  
    <param name="serial_baud_rate"   type="int"    value="115200"/>
...
```
## 啟動底盤
```
$ cd ackerman_ws/devel/
ackerman_ws/devel/$ source setup.bash
ackerman_ws/devel/$ roslaunch turn_on_wheeltec_robot base_serial.launch
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
