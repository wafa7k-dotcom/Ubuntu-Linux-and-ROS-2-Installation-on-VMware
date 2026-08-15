# Ubuntu-Linux-and-ROS-2-Installation-on-VMware
Documents installing Ubuntu 22.04 on VMware Workstation and setting up ROS 2 Humble Desktop — network setup, package updates, ROS repository configuration, environment sourcing, and verification via ros2 topic list, with problems faced and solutions.

Ubuntu Linux and ROS 2 Installation on VMware 

Project Overview 

This task demonstrates the installation of Ubuntu Linux using VMware Workstation 17 Player and the setup of ROS 2 Humble. 

The main goal was to create a Linux virtual machine, configure its network connection, update the operating system, install ROS 2, and verify that ROS 2 was working successfully. 

 

Tools and Software Used 

VMware Workstation 17 Player 

Ubuntu Linux — Ubuntu 22.04 Jammy 

ROS 2 Humble 

Terminal 

Internet connection 

 

1. Running Ubuntu on VMware 

Ubuntu was launched successfully inside VMware Workstation. 

The virtual machine provided an isolated Linux environment without affecting the main Windows operating system. 

Ubuntu was initially started through VMware and the desktop environment loaded successfully. 

 

2. Checking the Network Connection 

Before installing ROS 2, I checked whether Ubuntu had a working network connection. 

The following command was used: 

ip a 

This command displayed the available network interfaces and confirmed that the virtual machine received an IP address. 

Then, the Internet connection was tested using: 

ping -c 4 8.8.8.8 

and: 

ping -c 4 google.com 

The connection was successful and the packets were received without packet loss. 

 

3. Checking the Network Route 

The routing configuration was checked using: 

ip route 

This helped confirm that the Ubuntu virtual machine had a default network route and could access external networks. 

 

4. Updating Ubuntu Packages 

Before installing ROS 2, the Ubuntu package repositories were updated. 

sudo apt update 

Then, the installed packages were upgraded using: 

sudo apt upgrade -y 

This step downloaded and installed the available system updates. 

 

5. Preparing Ubuntu for ROS 2 

The required Ubuntu repository was enabled: 

sudo add-apt-repository universe 

Then the package list was updated again: 

sudo apt update 

The ROS repository key was added using: 

sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key \ 

  -o /usr/share/keyrings/ros-archive-keyring.gpg 

The ROS 2 repository was then added to Ubuntu. 

echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null 

After adding the repository: 

sudo apt update 

 

6. Installing ROS 2 Humble 

ROS 2 Humble Desktop was installed using: 

sudo apt install ros-humble-desktop -y 

This installed ROS 2 together with its main desktop tools and dependencies. 

 

7. Configuring ROS 2 Environment 

After the installation, the ROS 2 environment was loaded using: 

source /opt/ros/humble/setup.bash 

To automatically load ROS 2 whenever a new terminal is opened, the following command can also be used: 

echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc 

Then: 

source ~/.bashrc 

 

8. Testing ROS 2 

To verify that ROS 2 was installed successfully, the available ROS topics were checked using: 

ros2 topic list 

The terminal displayed ROS 2 topics such as: 

/parameter_events 

/rosout 

This confirmed that ROS 2 Humble was installed and running successfully. 

 

Problems Faced 

1. No Internet Connection 

One of the first problems was that the Ubuntu virtual machine did not initially have a working Internet connection. 

Because ROS 2 requires downloading packages from online repositories, the installation could not continue without network access. 

Solution 

The VMware network configuration was checked and the Ubuntu connection was verified using: 

ip a 

ip route 

ping -c 4 8.8.8.8 

ping -c 4 google.com 

After fixing the network connection, Ubuntu was able to access the Internet successfully. 

 

2. Large Number of Ubuntu Updates 

When running: 

sudo apt update 

Ubuntu showed that hundreds of packages could be upgraded. 

Solution 

The system was updated using: 

sudo apt upgrade -y 

The upgrade required some time because many system packages and dependencies needed to be downloaded and installed. 

 

3. ROS 2 Repository Was Not Available by Default 

ROS 2 Humble could not be installed directly before configuring the ROS repository. 

Solution 

The Ubuntu universe repository was enabled, the ROS key was added, and the official ROS 2 repository was configured before installing ROS 2 Humble. 

 

4. ROS Environment Needed to Be Loaded 

After installing ROS 2, ROS commands require the ROS environment to be sourced. 

Solution 

The following command was executed: 

source /opt/ros/humble/setup.bash 

It can also be added to .bashrc so it loads automatically every time the terminal starts. 

 

Final Result 

The task was completed successfully. I was able to: 

Run Ubuntu Linux using VMware Workstation. 

Configure the virtual machine network. 

Connect Ubuntu to the Internet. 

Update and upgrade Ubuntu packages. 

Configure the ROS 2 repository. 

Install ROS 2 Humble Desktop. 

Configure the ROS 2 environment. 

Run ROS 2 commands successfully. 

 

The final verification was performed using: 

ros2 topic list 

The output showed: 

/parameter_events 

/rosout 

Therefore, Ubuntu Linux and ROS 2 Humble were successfully installed and configured on VMware Workstation. 

 

Screenshots 

The screenshots used in this documentation are stored inside the images directory: 

images/ 

├── 01-ubuntu-vmware.jpg 

├── 02-network-test.jpg 

├── 03-apt-update.jpg 

├── 04-ubuntu-upgrade.jpg 

├── 05-packages-update.jpg 

├── 06-package-installation.jpg 

├── 07-ros-repository.jpg 

└── 08-ros2-test.jpg 

 
<img width="1280" height="720" alt="01-ubuntu-vmware" src="https://github.com/user-attachments/assets/3e93e894-fb61-4187-a046-e391f015df1d" />

Figure 1 – Ubuntu desktop running inside VMware Workstation 

 <img width="1280" height="720" alt="02-network-test" src="https://github.com/user-attachments/assets/21a0b5fb-430e-48fa-b7fb-249dabeef820" />


Figure 2 – Network configuration test (ip a, ping) 

 
<img width="1280" height="720" alt="03-apt-update" src="https://github.com/user-attachments/assets/0b0f7241-b657-4dbe-986d-96ce9ce211d8" />

Figure 3 – Running sudo apt update 

 
<img width="1280" height="720" alt="04-ubuntu-upgrade" src="https://github.com/user-attachments/assets/32ff1139-aa6f-4a96-bb0f-53427db85882" />

Figure 4 – Running sudo apt upgrade -y 

 
<img width="1280" height="720" alt="05-packages-update" src="https://github.com/user-attachments/assets/7cb6c9ea-0c52-4cf4-b7d9-9ca93b81dcff" />

Figure 5 – Package list update in progress 

 
<img width="1280" height="720" alt="06-package-installation" src="https://github.com/user-attachments/assets/d2fd0009-34f5-48f7-a0aa-674dd858a654" />

Figure 6 – Package installation in progress 

 
<img width="1280" height="720" alt="07-ros-repository" src="https://github.com/user-attachments/assets/8f171e3e-3db1-42fe-8148-da33ec8f2167" />

Figure 7 – Configuring the ROS 2 repository and installing ros-humble-desktop 

 
<img width="1280" height="720" alt="08-ros2-test" src="https://github.com/user-attachments/assets/4d1f4a68-05e1-4c4f-a3c3-de627dfa762b" />

Figure 8 – Final verification with ros2 topic list 

 

References 

ROS 2 Humble documentation: https://docs.ros.org/en/humble/ 

ROS 2 Ubuntu installation guide: https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debs.html 

Ubuntu documentation: https://help.ubuntu.com/ 

VMware documentation: https://docs.vmware.com/ 
