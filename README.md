# ERPNext ON Docker Installtion Guide

Proven Step by Step Guide for ERPNext Installation on Docker

## Prequsites:
- docker
- vscode
- Install Dev Containers for VSCode 
- wsl (windows subsystem for linux)  
- docker-compose (for Linux/mac)
- user added to docker group (for Linux/mac)

## Steps:

### Step 1: Clone and change directory to frappe_docker directory
Use commands: 
```shell
git clone https://github.com/frappe/frappe_docker.git zatca-dev
cd zatca-dev
```

### Step 2: Copy example devcontainer config from `devcontainer-example` to `.devcontainer`

```shell
cp -R devcontainer-example .devcontainer
```

### Step 3: Copy example vscode config for devcontainer from `development/vscode-example` to `development/.vscode`. This will setup basic configuration for debugging.

```shell
cp -R development/vscode-example development/.vscode
```

### Step 4: Open frappe_docker folder in VS Code.

```shell
code .
```

### Step 5:  `Dev Containers: Reopen in Container`. 

- Launch the command, from Command Palette (Ctrl + Shift + P) `Dev Containers: Reopen in Container`. You can also click in the bottom left corner to access the remote container menu.

- wait for its loading

#### expect to see the container in vscode like the following:
![image](imgs/first_container.png)

### step 6: Make sure files `installer.py` and `apps-example.json` are set to LF Not CRLF
![image](imgs/LF.png)
- 1 open the file
- 2 click on `CRLF`below 
- 3 Select LF from the upper window
- 4 save the file
- 5 repeat steps with `apps-example.json`

### Step 7: inside vscode open a new terminal in the container `Terminal Menu -> New Terminal`

### Step 8: run installer.py

- inside the terminal run:
 ```shell
python installer.py
```
- Don't close the terminal - wait for frappe and erpnext installation finish. -it may take a lot of time

### Step 8: Start Bench
- run commands:
 ```shell
cd frappe-bench
bench start
```
- Test frappe and erpnext
    - open `development.localhost:8000` in browser
    - use credintials: `Administrator` : `admin` to login
    - complete installation of frappe
        - Time Zone : `Asia/Riyadh`
        - Currency  : `SAR`
    - click next
    - company name : `Appy Innovate`
    - click `complete setup`
## Congratulations! Now You have your erpnext on Docker

- ----------------------------------------------------

# Steps To Install zatca Customization app:


## Confiigure Git with your company GitHub account via SSH

### Step 1: Make SSH Key:
- Use bech virtual env:
```shell
source frappe-bench/env/bin/activate
```
![image](https://github.com/Mohamed-Eid-Appy/ERPNext-Docker-Installtion-Guide/assets/170640563/56a7f21e-276b-4ee6-8032-713183b8e3f9)

- run this command to create the ssh key:
```shell
ssh-keygen -t rsa -b 4096 -C "MyEmail@appyinnovator.com" #change MyEmail@appyinnovator.com with your company github email
```

press enter, enter, enter
![image](https://github.com/Mohamed-Eid-Appy/ERPNext-Docker-Installtion-Guide/assets/170640563/36bd8684-8776-4885-a1e1-092e20f266d0)

- Add SSH Key to SSH Agent:
  - Start the SSH agent in the background:
  ```shell
  eval "$(ssh-agent -s)"
  ```
  - Add your SSH private key to the SSH agent:
  ```shell
  ssh-add ~/.ssh/id_rsa
  ```
  ![image](https://github.com/Mohamed-Eid-Appy/ERPNext-Docker-Installtion-Guide/assets/170640563/8864eca1-ce07-4e73-8b75-640a5e0d49e6)

- Add SSH Key to GitHub Account:
  - Copy the SSH key to your clipboard:
  ```shell
  cat ~/.ssh/id_rsa.pub
  ```
   copy  the result of previous command (Like the selected in the image below)
  ![image](https://github.com/Mohamed-Eid-Appy/ERPNext-Docker-Installtion-Guide/assets/170640563/34f9b3dc-a165-43b4-ae03-712acbce2a5e)

  - Go to GitHub > Settings > SSH and GPG keys > New SSH key, and paste the key and give it a name and click Add ssh Key.
    ![image](https://github.com/Mohamed-Eid-Appy/ERPNext-Docker-Installtion-Guide/assets/170640563/78ea444f-b5f6-405b-ae1f-fe0faf906c9a)
  - Go back to terminal and make sure you're authenticated:
    run the command:
    ```shell
    ssh -T git@github.com
    ```
    you should see a welcome message like this:
    ![image](https://github.com/Mohamed-Eid-Appy/ERPNext-Docker-Installtion-Guide/assets/170640563/efb8016f-1e16-4300-8029-a0fc903bef6a)
    #### congraulations Your Git is now connected to tour company Github Account!

### Step 2: install zatca app on your bench:
- run the command:
  ```shell
  bench get-app git@github.com:readerorg/ERPNext-Zatca.git
  ```
  ![image](https://github.com/Mohamed-Eid-Appy/ERPNext-Docker-Installtion-Guide/assets/170640563/a2155dd8-96c7-4355-8ffd-8732dd337dca)
