# Arktos deployment with Mizar CNI

## Prepare lab machine
### The preferred OS is Ubuntu 18.04.
### For AWS, the recommended instance size is t2.2xlarge and the storage size is 128GB or more.

## Steps:

### 1. Check the kernel version:
### Command:
```bash
uname -a
```
### Output:
![](images/img_16.png)

#### Update the kernel if the kernel version is below 5.6.0-rc2.

### Command:
```bash
wget https://raw.githubusercontent.com/CentaurusInfra/mizar/dev-next/kernelupdate.sh

sudo bash kernelupdate.sh
```
### Output:
![](images/img_17.png)

![](images/img_18.png)

#### Recheck Kernel version
### Command:
```bash
uname -a
```
### Output:
![](images/img_19.png)

### 2. Clone the Arktos repository and install the required dependencies:

### Command:
```bash
git clone https://github.com/Click2cloud-Centaurus/arktos.git ~/go/src/k8s.io/arktos -b default-cni-mizar

cd ~/go/src/k8s.io/arktos

git checkout default-cni-mizar

sudo bash ./hack/setup-dev-node.sh
```
### Output:
![](images/img_20.png)

![](images/img_21.png)



### Command:
```bash
echo export PATH=$PATH:/usr/local/go/bin\ >> ~/.profile

echo cd \$HOME/go/src/k8s.io/arktos >> ~/.profile

source ~/.profile
```

### Output:
![](images/img_22.png)

### 3. Start Arktos cluster without CNI Mizar

### Command:
```bash
CNIPLUGIN=mizar ./hack/arktos-up.sh
```
### Output:
![](images/img_23.png)

### Check Mizar Pods:

### Command:
```bash
./cluster/kubectl.sh get pod
```
### Output:
![](images/img_24.png)

### Check Nodes:
### Command:
```bash
./cluster/kubectl.sh get nodes
```

### Output:
![](images/img_25.png)

### Deploy net pods through yaml file

### Command:
```bash
vi netpod.yaml

./cluster/kubectl.sh apply -f netpod.yaml

```
### Output:
![](images/img_12.png)

### Check deployed pods
### Command:
```bash
./cluster/kubectl.sh get pods
```

### Output:
![](images/img_26.png)

### Check Ping for the deployed pods

### Command:
```bash
./cluster/kubectl.sh get pods -o wide

./cluster/kubectl.sh exec [Pod name] ping [ip]
```
### Output:
![](images/img_27.png)

### Deployed pods got stucked in the container creation state.

### Ckeck VPCs
### Command:
```bash
./cluster/kubectl.sh get vpcs
```
### Output:
![](images/img_28.png)

### Check Subnets
### Command:
```bash
./cluster/kubectl.sh get subnets
```
### Output:
![](images/img_29.png)

## Passed



