## Scenario 1:
# Arktos deployment without Mizar CNI

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
![](images/img_1.png)

#### Update the kernel if the kernel version is below 5.6.0-rc2.

### Command:
```bash
wget https://raw.githubusercontent.com/CentaurusInfra/mizar/dev-next/kernelupdate.sh

sudo bash kernelupdate.sh
```
### Output:
![](images/img_2.png)

![](images/img_3.png)

#### Recheck Kernel version
### Command:
```bash
uname -a
```
### Output:
![](images/img_4.png)

### 2. Clone the Arktos repository and install the required dependencies:

### Command:
```bash
git clone https://github.com/Click2cloud-Centaurus/arktos.git ~/go/src/k8s.io/arktos -b default-cni-mizar

cd ~/go/src/k8s.io/arktos

git checkout default-cni-mizar

sudo bash ./hack/setup-dev-node.sh
```
### Output:
![](images/img_5.png)

![](images/img_6.png)

![](images/img_7.png)

### Command:
```bash
echo export PATH=$PATH:/usr/local/go/bin\ >> ~/.profile

echo cd \$HOME/go/src/k8s.io/arktos >> ~/.profile

source ~/.profile
```

### Output:
![](images/img_8.png)

### 3. Start Arktos cluster without CNI Mizar

### Command:
```bash
./hack/arktos-up.sh
```
### Output:
Error on first execution
![](images/img_9.png)

Arktos got up after second execution
![](images/img_10.png)

### Check Nodes:

### Command:
```bash
./cluster/kubectl.sh get nodes
```
### Output:
![](images/img_11.png)

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
![](images/img_13.png)

### Check Ping for the deployed pods

### Command:
```bash
./cluster/kubectl.sh get pods -o wide

./cluster/kubectl.sh exec [Pod name] ping [ip]
```
### Output:
![](images/img_14.png)

![](images/img_15.png)

## Pass

## Scenario 2:
# Arktos deployment with Mizar CNI

### 1. Check Kernal version
### Command:
```bash
uname -a
```
### Output:
![](images/img_30.png)

### 2. Clone the Arktos repository and install the required dependencies:

### Command:
```bash
git clone https://github.com/Click2cloud-Centaurus/arktos.git ~/go/src/k8s.io/arktos -b default-cni-mizar

cd ~/go/src/k8s.io/arktos

git checkout default-cni-mizar

sudo bash ./hack/setup-dev-node.sh
```
### Output:
![](images/img_31.png)

### Command:
```bash
echo export PATH=$PATH:/usr/local/go/bin\ >> ~/.profile
echo cd \$HOME/go/src/k8s.io/arktos >> ~/.profile
source ~/.profile
```
### Output:
![](images/img_32.png)

### 3. Start Arktos cluster
### Command:
```bash
CNIPLUGIN=mizar ./hack/arktos-up.sh
```
### Output:
![](images/img_33.png)

### Check nodes
### Command:
```bash
./cluster/kubectl.sh get nodes
```
### Output:
![](images/img_34.png)

### Check Mizar Pods
### Command:
```bash
./cluster/kubectl.sh get pods
```

### Output:
![](images/img_35.png)

### Deploy net pods

### Command:
```bash
./cluster/kubectl.sh apply -f netpod.yaml
```
### Output:
![](images/img_36.png)

### Check deployed pods
### Command:
```bash
./cluster/kubectl.sh get pods
```
### Output:
![](images/img_37.png)
 ### Deployed pods got stuck in container creation state

 ### Check VPCs
 ### Command:
 ```bash
 ./cluster/kubectl.sh get vpcs
 ```
 ### Output:
 ![](images/img_38.png)

 ### Check Subnets:
 ### Command:
 ```bash
 ./cluster/kubectl.sh get subnets
 ```
### Output:
![](images/img_39.png)

## Pass

### Scenario 3:
# Arktos deployment without Mizar CNI after deployment with Mizar CNI.

### 1. Check Kernal version
### Command:
```bash
uname -a
```
### Output:
![](images/img_40.png)

### 2. Clone the Arktos repository and install the required dependencies:
### Command:
```bash 
git clone https://github.com/Click2cloud-Centaurus/arktos.git ~/go/src/k8s.io/arktos -b default-cni-mizar

cd ~/go/src/k8s.io/arktos

git checkout default-cni-mizar

sudo bash ./hack/setup-dev-node.sh
```
### Output:
![](images/img_41.png)

### Command:
```bash
echo export PATH=$PATH:/usr/local/go/bin\ >> ~/.profile
echo cd \$HOME/go/src/k8s.io/arktos >> ~/.profile
source ~/.profile
```
### Output:
![](images/img_42.png)

### 3. Start Arktos cluster
### Command:
```bash
 ./hack/arktos-up.sh
```
### Output:
![](images/img_44.png)

### Check Nodes
### Command:
```bash
./cluster/kubectl.sh get nodes
```
### Output:
![](images/img_43.png)

### Deploy net pods

### Command:
```bash
./cluster/kubectl.sh apply -f netpod.yaml
```
### Output:
![](images/img_45.png)

### Check Deployed pods
### Command:
```bash
./cluster/kubectl.sh get pods
```
### Output:
![](images/img_46.png)

### Deployed pods got stuck in Container creation state.

## Fail


