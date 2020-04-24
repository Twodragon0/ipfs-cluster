
## Go,IPFS Install
```sh
wget -q -O - https://raw.githubusercontent.com/canha/golang-tools-install-script/master/goinstall.sh | bash
source /home/$USER/.bashrc
wget https://dist.ipfs.io/go-ipfs/v0.4.23/go-ipfs_v0.4.23_linux-amd64.tar.gz
tar -xvzf go-ipfs_v0.4.23_linux-amd64.tar.gz
cd go-ipfs
sudo ./install.sh
```
If not work,move the binary somewhere in your `$PATH`:
```sh
sudo mv ipfs /usr/local/bin/ipfs
```
## ipfs-cluster Install

```sh
git clone https://github.com/ipfs/ipfs-cluster.git
cd ipfs-cluster
export GO111MODULE=on # optional, if checking out the repository in $GOPATH.
go install ./cmd/ipfs-cluster-service
go install ./cmd/ipfs-cluster-ctl
go install ./cmd/ipfs-cluster-follow
```

## Usage for Private Network
First, you must initialize and run your local ipfs node:

```sh
rm -rf ~/.ipfs/
ipfs init
sudo nano ~/.ipfs/swarm.key
```
Put in swarm.key copy 
Reference: https://https://tstrs.me/en/1459.htmltstrs.me/en/1459.html

```sh
ipfs bootstrap rm all
ipfs bootstrap add /ip4/192.241.213.72/tcp/4001/ipfs/QmcJw57d1X38X4kknLWHh4gKNhB4yfj9cQitwQpCEFFdz5
ipfs daemon &
ipfs swarm peers
```
This will give you directions to get started with ipfs private network.

## Usage for IPFS-Cluster in Private Network
Put in Follow_service.json file.
```sh
ipfs-cluster-service init --consensus crdt
sudo rm -rf ~/.ipfs-cluster/service.json
sudo nano ~/.ipfs-cluster/service.json
```
ipfs-cluster-service mode.
```sh
ipfs-cluster-service daemon
```
or 
ipfs-cluster-follow mode.
```sh
ipfs-cluster-follow ipfs-cluster run --init http://127.0.0.1:8080/ipfs/Qme9W5kY8iL7xUo1r61HC83453jW6zrRu9Eefqh3DAx4Yj
```
## Error solutions
ipfs daemon for private network solutions:
- Error: serveHTTPApi: manet.Listen(/ip4/127.0.0.1/tcp/5001) failed: listen tcp4 127.0.0.1:5001: bind: address already in use
- Error: serveHTTPGateway: manet.Listen(/ip4/127.0.0.1/tcp/8080) failed: listen tcp4 127.0.0.1:8080: bind: address already in use
```sh
netstat -ano | grep 5001
kill $(lsof -t -i:5001)
```
```sh
sudo lsof -i :8080
sudo kill -9 $PID
```
