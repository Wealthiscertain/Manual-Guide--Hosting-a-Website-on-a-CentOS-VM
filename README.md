# Manual-Guide-Hosting-a-Website-on-a-CentOS-VM

In my previous article, I provided a [Step-by-Step Guide to Creating a CentOS VM with Vagrant](https://medium.com/@wealthiscertain/step-by-step-guide-to-creating-a-centos-vm-with-vagrant-9b67ccb5916e). In this post, I'll walk you through the process of hosting an HTML template on CentOS with the help of **httpd** on a Vagrant-managed VM.

**Tools used**
**- Ready-made template:** Free HTML website templates from [tooplate.com]
**- Vagrant:** Automates the creation and management of virtual environments.
**- CentOS:** A free, enterprise-class Linux distribution, ideal for server environments.
**- Git Bash:** A command-line tool that allows users to run Git commands and other Unix-based utilities on Windows.

**Step-by-Step Setup**

**1. Create and Initialize a Vagrant Directory**
   
- Navigate to your **vagrant-vms** directory and create a new directory named **finance** using the command **mkdir finance**.

  ![image](https://github.com/user-attachments/assets/d27b0695-bf0c-40df-bdcd-6d8d337ef645)

- Initialize Vagrant in this directory with: **vagrant init eurolinux-vagrant/centos-stream-9**.

  ![image](https://github.com/user-attachments/assets/e166ccd5-f4b9-4932-aab2-3d6cf560030c)

**2. Configure the Vagrantfile**

- Open the Vagrantfile in the **finance** directory with **vim Vagrantfile**.

  ![image](https://github.com/user-attachments/assets/30c957d6-c73f-4917-9890-b7cdfb4dad9e)

- Press **i** to enter insert mode, then uncomment and modify the lines for the IP address and memory size. Change the IP from **192.168.33.10** to **192.168.56.22**.

**Before**
  
  ![image](https://github.com/user-attachments/assets/4cc65c2c-2556-4295-8359-ffabb4023318)

**After**

  ![image](https://github.com/user-attachments/assets/cac0ce14-0f56-407b-ae70-3595add9ae5c)

- Press **esc** button on your PC to switch back to **command mode**.
- Type **:wq** to save and exit the file.

**3. Launch the VM**
- Start the VM with the command **vagrant up**.

  ![image](https://github.com/user-attachments/assets/3399166f-a3f7-4214-bccc-576a615d8a48)

- Once the VM is up, log in to the VM with the **vagrant ssh** command.

  ![image](https://github.com/user-attachments/assets/1d0be8b0-5e93-4f0c-89f9-a47e4ad4a630)

- Switch to the root user by running **sudo -i**.

  ![image](https://github.com/user-attachments/assets/b711d9a0-4bbc-4c48-9190-917ce48f4bad)

**4. Update the VM Hostname**
- Change the hostname by editing the **/etc/hostname** file with **vi /etc/hostname**.
- **vi:** is the default editor that comes with the LINUX operating system.

  ![image](https://github.com/user-attachments/assets/2c63cdc1-73e6-4594-a296-056e92541458)

- Once the editor is up, type the new name, and type **:wq** to save and exit the vim editor.

  ![image](https://github.com/user-attachments/assets/55233d86-2f61-453c-b260-96ab5d8f7ed2)

- Apply the new hostname by running **hostname finance**.

**5. We will require the following packages:**
**- httpd:** The package is needed to host websites on CentOS.
**- wget:** A tool for downloading files, such as HTML templates.
**- vim:** A text editor for modifying files.
**- unzip:** A utility for extracting files from ZIP archives.

**6. Install necessary packages**
- Install the required packages using the command: **yum install httpd wget vim unzip zip -y**.
- The **complete** message at the end signifies the installation was Successful.

  ![image](https://github.com/user-attachments/assets/9be6099c-2f36-43a2-ae79-2889cbe55708)

**7. Start the httpd Service**
- Start and enable the **httpd** service with the following commands:
    **- systemctl start httpd**
    **- systemctl enable httpd**

  ![image](https://github.com/user-attachments/assets/830a8d23-eabc-4a4e-af60-0772d31bdafb)

**8. Check the VM's IP Address**
- Verify the IP address with **ip addr show**.

  ![image](https://github.com/user-attachments/assets/dcccd095-b23c-4f63-9cc0-6cb6990a9b66)

- Test access by navigating to **http://192.168.56.22/** in your web browser.

  ![image](https://github.com/user-attachments/assets/e1d3af0c-3ebd-4af8-b637-20acf57255bd)

**9. Download an HTML Template**
- Select a free HTML website template from [tooplate.com], For this project, I chose the [Mini finance template](https://www.tooplate.com/view/2135-mini-finance).

  ![image](https://github.com/user-attachments/assets/6e3abc33-fc40-4b1e-9d1a-4c9eb9baad9c)

- Copy the download link from the browser's developer tools (F12).

  ![image](https://github.com/user-attachments/assets/56c4cb12-d7c9-464b-93fa-613d091a71e4)

  ![image](https://github.com/user-attachments/assets/a3839e35-8e83-402c-bdda-6fb47cdedd32)

**10. Download and Extract the Template**
- Navigate to the HTML folder with **cd var/www/html/**
- Navigate to the directory to the **tmp** directory with **cd /tmp/**
- Download the template using **wget https://www.tooplate.com/zip-templates/2135_mini_finance.zip**

  ![image](https://github.com/user-attachments/assets/9b3b375d-4ef4-4a00-a3a4-ba961e57b155)

- Unzip the downloaded file with **unzip 2135_mini_finance.zip**

  ![image](https://github.com/user-attachments/assets/a1cf66fa-8a19-430f-a482-e99feff5f824)

- Confirm operation was successful

  ![image](https://github.com/user-attachments/assets/85fee597-b469-477c-b9e4-cc53192ae771)

**11. Deploy the Template to the Web Server**
- Use command **cd 2135_mini_finance** to navigate to the HTML template directory
- Copy the template files to the web server's root directory with **cp -r * /var/www/html/**
- Confirm copy was successful

  ![image](https://github.com/user-attachments/assets/dbbdc74a-989c-4ee1-a346-515ba9150723)

**12. Restart the httpd Service**
- Ensure the **httpd** service is running smoothly by restarting it and checking its status:
  
   **- systemctl start httpd**
   **- systemctl status httpd**

**13. Verify the Website**
Visit **http://192.168.56.22/** in your browser to confirm the website is up and running.

  ![image](https://github.com/user-attachments/assets/cda29ca1-a816-4ff0-a99b-0aff5fc375fe)

