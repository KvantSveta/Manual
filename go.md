# Install Go1.9 on Raspberry Pi

**download go1.9 and install**

```bash
mkdir go1.9
cd go1.9
wget https://storage.googleapis.com/golang/go1.9.linux-armv6l.tar.gz
tar -xvzf go1.9.linux-armv6l.tar.gz
sudo cp -r go /usr/local
export PATH=$PATH:/usr/local/go/bin
```

or

```bash
wget https://storage.googleapis.com/golang/go1.9.linux-armv6l.tar.gz
sudo tar -C /usr/local -xzf go1.9.linux-armv6l.tar.gz
export PATH=$PATH:/usr/local/go/bin
```

**update ~/.profile**

```bash
nano ~/.profile
export PATH=$PATH:/usr/local/go/bin
```

**add GOPATH and GOROOT on Windows**

```bash
export GOROOT=/d/Go
export GOPATH=/d/Go
export PATH=$PATH:$GOROOT/bin:$GOPATH/bin
or
export PATH=$PATH:/d/Go/bin
```

**add GOPATH on Linux**

```bash
export GOPATH=$HOME/go
```

> GOROOT must be set only when installing to a custom location

**add on .zshrc**

```bash
export GOPATH=$HOME/go
```

**download dependencies**

```bash
# download src and compill static library go-rpio.a in pkg
go get "github.com/stianeikeland/go-rpio"

# only download src files
go get -d "github.com/stianeikeland/go-rpio"
```
