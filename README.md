## 環境構築
- WSL上でUbuntu起動
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
