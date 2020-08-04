# RPI-docker-setup

## Prepare SD CARD

- install Lite version on sd using **imager** from [here](https://www.raspberrypi.org/downloads/) 

- enable ssh
  
  - add ssh file (no extension) on boot partition (small one)
  
- setup wifi.

  - generate psk encrypted key.

    - generate key from bash: 

      ```
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

## Insert card in RPI and boot

- connect through ssh

  ```
  ssh pi@<pi_adress>
  ```

- default password is **raspberry**

- change password !

  ```
  passwd
  ```

- update and upgrade

  ```
  sudo apt update
  sudo apt dist-upgrade
  ```

- setup small things

  ```
  sudo raspi-config
  ```

  - enable ssh for good : go to Interfacing Options / ssh --> enable
  - Use all sd card space: go to Advanced Options / Expand Filesystem

- reboot

- check partition sizes

  ```
  df
  ```

- shutdown

  ```
  sudo shutdown -h now
  ```

## Setup Python

- check python version

  ```
  python3 --version
  ```

- install pip / venv

  ```
  sudo apt install python3-pip
  sudo apt install python3-venv
  ```

## Install Docker

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

## Install / Setup Git

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

  

