# Arktos deployment with Mizar CNI (With default-cni-mizar branch)

### Prepare lab machine, the preferred OS is Ubuntu 18.04. If you are using AWS, the recommended instance size is t2.2xlarge and the storage size is 128GB or more.

## Steps:

### 1. Check the kernel version:
### Command:
```bash
uname -a
```
### Output:
![](images/img_12.png)

#### Update the kernel if the kernel version is below 5.6.0-rc2

### Command:
```bash
wget https://raw.githubusercontent.com/CentaurusInfra/mizar/dev-next/kernelupdate.sh

sudo bash kernelupdate.sh
```
### Output:
![](images/img_13.png)

![](images/img_14.png)

![](images/img_15.png)

### 2. Clone the Arktos repository and install the required dependencies:

### Command:
```bash
git clone https://github.com/CentaurusInfra/arktos.git ~/go/src/k8s.io/arktos 

sudo bash $HOME/go/src/k8s.io/arktos/hack/setup-dev-node.sh

echo export PATH=$PATH:/usr/local/go/bin\ >> ~/.profile

echo cd \$HOME/go/src/k8s.io/arktos >> ~/.profile

source ~/.profile
```
### Output:
![](images/img_16.png)

![](images/img_17.png)

![](images/img_18.png)

### 3. Start Arktos cluster
### Command:
```bash
CNIPLUGIN=mizar ./hack/arktos-up.sh
```
### Output:
![](images/img_19.png)

#### Git remote:
![](images/img_20.png)

## Failed
