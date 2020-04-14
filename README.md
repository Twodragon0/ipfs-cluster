# ipfs commandline tool

This is the [ipfs](http://ipfs.io) commandline tool. It contains a full ipfs node.

## Go, IPFS Install
```sh
wget -q -O - https://raw.githubusercontent.com/canha/golang-tools-install-script/master/goinstall.sh | bash
source /home/$USER/.bashrc
https://dist.ipfs.io/go-ipfs/v0.4.23/go-ipfs_v0.4.23_linux-amd64.tar.gz
tar xvfz go-ipfs.tar.gz
cd go-ipfs
./install.sh
```
If not work,move the binary somewhere in your `$PATH`:
```sh
sudo mv ipfs /usr/local/bin/ipfs
```
## Usage
First, you must initialize and run your local ipfs node:

```sh
ipfs init
ipfs daemon &
```
This will give you directions to get started with ipfs.
You can always get help with:

```sh
ipfs --help
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
