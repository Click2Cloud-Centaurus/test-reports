# Arktos deployment with Mizar CNI (With cni-mizar branch)
### Prepare lab machine, the preferred OS is Ubuntu 18.04. If you are using AWS, the recommended instance size is t2.2xlarge and the storage size is 128GB or more.

## Steps:

### 1. Check the kernel version:

### Command:
```bash
uname -a
```
### Output:
![](images/img_1.png)

#### Update the kernel if the kernel version is below 5.6.0-rc2

### Command:
```bash
wget https://raw.githubusercontent.com/CentaurusInfra/mizar/dev-next/kernelupdate.sh

sudo bash kernelupdate.sh
```
### Output:
![](images/img_2.png)

![](images/img_3.png)

![](images/img_4.png)

### 2. Clone the Arktos repository and install the required dependencies:
### Command:
```bash
git clone https://github.com/Click2Cloud-Centaurus/arktos.git ~/go/src/k8s.io/arktos

cd ~/go/src/k8s.io/arktos

git fetch origin pull/6/head:pr6

git checkout pr6

sudo bash ./hack/setup-dev-node.sh
```
### Output:
![](images/img_5.png)

![](images/img_6.png)

![](images/img_7.png)

![](images/img_8.png)

### Command:
```bash
echo export PATH=$PATH:/usr/local/go/bin\ >> ~/.profile

echo cd \$HOME/go/src/k8s.io/arktos >> ~/.profile

source ~/.profile
```
### Output:
![](images/img_9.png)

### 3. Start Arktos cluster
### Command:
``` bash
CNIPLUGIN=mizar ./hack/arktos-up.sh
```
### Output:
![](images/img_10.png)

### 4.Leave the "arktos-up.sh" terminal and open another terminal to the master node. Verify mizar pods i.e. mizar-operator and mizar-daemon pods are in running state, for that run:
### Command:
```bash
./cluster/kubectl.sh get pods
```
### Output:
![](images/img_11.png)

### Pods are in running state. 
## Passed.

