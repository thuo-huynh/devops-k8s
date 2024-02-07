### Windows Preparation

1. Ensure hypervisor functionality is enabled in BIOS.
   * I know it sounds stupid, but if you already have it enabled, disable it, restart the machine, and enable it again.
   * Otherwise you will hit https://github.com/microsoft/WSL/issues/5363
   
2. Launch a PowerShell prompt in Administrator mode [Win+X > Windows PowerShell (Admin)]

```
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
bcdedit /set hypervisorlaunchtype auto
```
3. Install the Linux kernel update package and install it
   * x86/x64 - https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi
   * arm64 - https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_arm64.msi

5. Restart machine

4. Launch a PowerShell prompt in Administrator mode [Win+X > Windows PowerShell (Admin)]

```
wsl --set-default-version 2
```

5. Install Ubuntu Linux distribution of your choice from the Windows Store (not the one with the version in the names)

6. Verify WSL version is set correctly

```
wsl --list --verbose
```

### Ubuntu Preparation

1. Run series of commands to get right build of Docker installed
   * Removes the old crap, gets the dependencies right, adds Docker key, adds Docker repo, installs the new hotness

```
sudo apt-get remove docker docker-engine docker.io containerd runc
sudo apt-get update
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
sudo apt-get update
sudo apt-get upgrade -y
sudo apt-get install docker-ce docker-ce-cli containerd.io -y
```

2. Run series of commands to ensure you can interact with Docker without root
   * Third command here is a trick to reload your profile without actually logging out
   * Closing out Ubuntu shell and starting over instead of third command is an option

```
sudo groupadd docker
sudo usermod -aG docker ${USER}
su -s ${USER}
```

3. Test the Docker configuration

```
sudo service docker start
docker run hello-world
```

If you have issues with the `docker run hello-world` command, see the `troubleshooting.md` on this gist.

### Minikube Preparation

1. Install Minikube

```
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube_latest_amd64.deb
sudo apt install ./minikube_latest_amd64.deb -y
rm minikube_latest_amd64.deb
```

2. Start it

```
minikube start
```

3. Get the dashboard going 
   * The dashboard will continue to run and does not return back to a prompt here
   * You will need to kill the dashboard to continue in the guide
   
```
minikube dashboard
```

4. Open the dashboard in your favorite browser (in Windows)
   * Port is dynamic, so can't document it well - you'll just have to be good at reading directions
   * The port will be in output of step 3 command
   * Should look something like this...

```
http://127.0.0.1:[PORT GOES HERE]/api/v1/namespaces/kubernetes-dashboard/services/http:kubernetes-dashboard:/proxy/#/workloads?namespace=default
```

5. This process is going to block you from the finishing this guide, but to keep it running, do the following...
   * Perform "CTRL+Z" on the keyboard to send the process into paused state
   * Execute the following command to resume the paused process in the background

```
bg
```

### Kubectl Preparation

1. Install Kubectl
   * Adds k8s key, adds k8s repo, installs the new hotness

```
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee -a /etc/apt/sources.list.d/kubernetes.list
sudo apt-get update
sudo apt-get install -y kubectl
```

2. Use it

```
kubectl get po -A
```

### Helm Preparation

1. Install Helm

```
curl --output helm-linux-amd64.tar.gz https://get.helm.sh/helm-v3.4.2-linux-amd64.tar.gz
tar -zxvf helm-linux-amd64.tar.gz
sudo mv linux-amd64/helm /usr/local/bin/helm
rm helm-linux-amd64.tar.gz
rm -rf linux-amd64
```

2. Use it

```
helm version
```