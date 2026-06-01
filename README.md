## 環境構築
- https://note.com/tanoshi_lab/n/n6b28d21fce2f
- https://zenn.dev/sakai13/books/7639959094542f
- https://independence-sys.net/main/?p=7444
### 直接インストール
```
locale
```
- UTF-8でない場合
```
$ sudo apt install locales
$ sudo locale-gen en_US en_US.UTF-8
$ sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
$ export LANG=en_US.UTF-8
```
- Universeリポジトリ有効化
```
$ sudo apt install software-properties-common
$ sudo add-apt-repository universe
```

- ROS2 GPGキー登録
```
$ sudo apt install curl -y
$ sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key \
-o /usr/share/keyrings/ros-archive-keyring.gpg
```
- ROS2リポジトリ追加
```
$ echo "deb [arch=$(dpkg --print-architecture) \
$ signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] \
$ http://packages.ros.org/ros2/ubuntu noble main" | \
$ sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
```
- 確認
```
$ cat /etc/apt/sources.list.d/ros2.list
deb [arch=amd64 signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu noble main
```
- 更新
```
sudo apt update
```
- フル（GUI含む）インストール
```
sudo apt install ros-jazzy-desktop -y
```
- 環境変数設定
```
$ echo "source /opt/ros/jazzy/setup.bash" >> ~/.bashrc
$ source ~/.bashrc
$ echo $ROS_DISTRO
jazzy
```
- 診断
```
ros2 doctor
```
### Dockerインストール
```
$ sudo apt-get update
$ sudo apt-get install ca-certificates curl
$ sudo install -m 0755 -d /etc/apt/keyrings
$ sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
$ sudo chmod a+r /etc/apt/keyrings/docker.asc
$ echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
$ sudo apt-get update

$ sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

$ sudo usermod -aG docker $USER
```
### 簡易的にDocker上でGUIのROS
- https://github.com/Tiryoh/docker-ros2-desktop-vnc
```
docker run -p 6080:80 --security-opt seccomp=unconfined --shm-size=512m ghcr.io/tiryoh/ros2-desktop-vnc:jazzy
```
- http://127.0.0.1:6080

## 通信方式
- ノード
### トピック通信
- 一方向通信
- Publisherからトピックを介してSubscriberに送信
- 流し続ける

### サービス通信
- 双方向通信
- クライアントとサーバーの間での通信
- すぐ終わる

### アクション通信
- トピック通信とサービス通信の組み合わせ
- アクションクライアントとアクションサーバーの通信
- 時間がかかる

## 動作確認
### パブリッシャ
- ターミナル1
```
ros2 run demo_nodes_py talker  
```
### サブスクライバー
- ターミナル2
```
ros2 run demo_nodes_py listener     
```
### グラフ
- ターミナル3
```
ros2 run rqt_graph rqt_graph
```

## ノード確認
```
ros2 node list
```

## シミュレーター
### Turtlesim
- 使用できるコマンド
```
ros2 pkg executables turtlesim
```
- シミュレーター起動
```
ros2 run turtlesim turtlesim_node
```
- キー入力によるリモート操作起動
```
ros2 run turtlesim turtle_teleop_key
```
