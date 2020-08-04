# RPI-Setup

## First Boot

### Prepare SD CARD

- install Lite version on sd using **imager** from [here](https://www.raspberrypi.org/downloads/) 

- enable ssh
  
  - add ssh file (no extension) on boot partition (small one)
  
- setup wifi (if pi board is wifi capable...)

  - generate psk encrypted key.

    - generate key from bash: 

      ```bash
      wpa_passphrase <SSID> <Password>
      ```

  - create file wpa_supplicant.conf on boot partition like this one

    ```
    ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
    update_config=1
    country=FR
    
    network={
     ssid="<SSID>"
     psk=<psk_key_generated_from_above>
    }
    ```

### Insert card in RPI and boot

- connect through ssh

  ```bash
  ssh pi@<pi_address>
  ```

- default password is **raspberry**

- change password !

  ```bash
  passwd
  ```

- update and upgrade

  ```bash
  sudo apt update
  sudo apt dist-upgrade
  ```

- setup small things

  ```bash
  sudo raspi-config
  ```

  - enable ssh for good : go to Interfacing Options / ssh --> enable
  - Use all sd card space: go to Advanced Options / Expand Filesystem

- reboot

### Tips

- check partition sizes

  ```bash
  df
  ```

- shutdown

  ```bash
  sudo shutdown -h now
  ```
  
- ssh connection using keys

  - generate keys from local computer

    ```bash
    ssh-keygen
    ```

  - key is generated in ~/.ssh/ named id_rsa (private key) and id_rsa_pub (public key to be copied to RPi)

  - Copy id to RPI

    ```bash
    ssh-copy-id pi@<pi_address>
    ```

  - Backup private key (just in case)

    ```bash
    cp ~/.ssh/id_rsa ~/<keyname.pem>
    ```

  - Disable ssh authentication by password on Rpi

    - Connect using key

    ```bash
    ssh -i <keyname.pem> pi@<pi_address>
    ```

    - Edit sshd_config

    ```bash
    sudo nano /etc/ssh/sshd_config
    ```

    - Uncomment and set to no, the line:

      To disable tunneled clear text passwords, change to no here!

    ```bash
    PasswordAuthentication no
    ```

    - Restart ssh service

    ```bash
    sudo service ssh restart
    ```

## Install softwares

### Setup Python

- check python version

  ```
  python3 --version
  ```

- install pip / venv

  ```
  sudo apt install python3-pip
  sudo apt install python3-venv
  ```

### Install Docker

- Download the script and install

  ```
  curl -fsSL https://get.docker.com -o get-docker.sh
  sudo sh get-docker.sh
  ```

- Add a Non-Root User to the Docker Group

  ```
  sudo usermod -aG docker [user_name]
  ```
  
- Install Docker Compose

  ```
  sudo pip3 install docker-compose
  ```

### Install / Setup Git

- install

  ```
  sudo apt install git-all
  ```

- setup

  ```
  git config --global user.name "My Name"
  git config --global user.email My@email
  ```

- check setup

  ```
  git config --list
  ```

  

