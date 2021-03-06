
## Go,IPFS Install
```sh
wget -q -O - https://raw.githubusercontent.com/canha/golang-tools-install-script/master/goinstall.sh | bash
source /home/$USER/.bashrc
wget https://github.com/ipfs/go-ipfs/releases/download/v0.6.0/go-ipfs_v0.6.0_linux-amd64.tar.gz
tar -xvzf go-ipfs_v0.6.0_linux-amd64.tar.gz
cd go-ipfs
sudo bash install.sh
ipfs --version
```
If not work,move the binary somewhere in your `$PATH`:
```sh
sudo mv ipfs /usr/local/bin/ipfs
```
## ipfs-cluster Install

Installing from source  
The following requirements apply to the installation from source:    
- Go 1.12+    
- Git   

```sh
git clone https://github.com/ipfs/ipfs-cluster.git
cd ipfs-cluster
export GO111MODULE=on # optional, if checking out the repository in $GOPATH.
go install ./cmd/ipfs-cluster-service
go install ./cmd/ipfs-cluster-ctl
go install ./cmd/ipfs-cluster-follow
```
If using raspberry pi, download from homepage:      
https://dist.ipfs.io/#ipfs-cluster-ctl   
And it should the same method (Choice go install or download from homepage)  

## Usage for Private Network
First, you must initialize and run your local ipfs node:

```sh
rm -rf ~/.ipfs/
ipfs init
sudo nano ~/.ipfs/swarm.key
```
Put in swarm.key copy 
Reference: https://tstrs.me/en/1459.html

```sh
ipfs bootstrap rm all
ipfs bootstrap add /ip4/192.*.*.*/tcp/4001/p2p/Qma4bvcDe5sXZbB*FtTv
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
ipfs-cluster-service mode:
```sh
ipfs-cluster-service daemon
```
or ipfs-cluster-follow mode:
```sh
ipfs-cluster-follow ipfs-cluster run --init http://127.0.0.1:8080/ipfs/Qme9W5kY8iL7xUo1r61*h3DAx4Yj
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

ERROR crdt: expected 1 as the cid version number, got: 10 crdt.go:308    
ERROR crdt: reading varint: buffer too small crdt.go:308     

https://discuss.ipfs.io/t/share-pin-and-data-using-ipfs-cluster-in-different-network/7792    

$sudo nano ~/.bashrc (#export GOPATH=/root/go export #GOROOT=/root/.go)

```sh
go clean ipfs-cluster-ctl
go clean ipfs-cluster-service
go clean ipfs-cluster-follow
wget https://dist.ipfs.io/ipfs-cluster-follow/v0.12.1/ipfs-cluster-follow_v0.12.1_linux-amd64.tar.gz
wget https://dist.ipfs.io/ipfs-cluster-service/v0.12.1/ipfs-cluster-service_v0.12.1_linux-amd64.tar.gz
wget https://dist.ipfs.io/ipfs-cluster-ctl/v0.12.1/ipfs-cluster-ctl_v0.12.1_linux-amd64.tar.gz
tar -xvzf ipfs-cluster-follow_v0.12.1_linux-amd64.tar.gz
tar -xvzf ipfs-cluster-service_v0.12.1_linux-amd64.tar.gz
tar -xvzf ipfs-cluster-ctl_v0.12.1_linux-amd64.tar.gz
cd ~/ipfs-cluster-follow
sudo mv ipfs-cluster-follow /usr/local/bin/
cd ~/ipfs-cluster-service
sudo mv ipfs-cluster-service /usr/local/bin/
cd ~/ipfs-cluster-ctl
sudo mv ipfs-cluster-ctl /usr/local/bin/
```
After clean, installation from homepage

## Testground file move using scp
```sh
scp -P 30000 /home/wrl/testground/312f91922027.tgz ny@161.*.*.*:~/
```
