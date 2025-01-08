# Productivity and Everyday Use

Efficiency in a Linux environment depends on acquiring the essential knowledge and tools that translate into a smooth workflow. This chapter will walk you through the steps of effective completion of day-to-day activities on Ubuntu, so you have productivity taken care of and peace of mind when dealing with the vital configurations of the system.  

We'll discuss some important issues: from setting up your hostname and time, date, and NTP services to keep the system time accurate; basic management of users by adding them to a system with the appropriate rights to update and upgrade the system so as to keep it secured and stable.

Along with system setup, this chapter covers some common productivity-enhancing tools. This section is designed to help you better navigate your way through operating under the Linux-based workflow by looking into office suites to create and manage documents and using collaboration tools to stay connected with a team. Whether you have never done these tasks or are trying to improve, this chapter is going to guide you further in bringing productivity within Ubuntu.

Let’s dive in and see how Ubuntu simplifies the management of these everyday operations.

## Configure hostname,Time, date and NTP configurations.

We will discuss how to set up the hostname, time, date, and NTP settings on an Ubuntu system in this part. Take the appropriate actions in each.

### Configure hostname

Hostnames are important for identifying systems on a network. Whether you’re working with a single machine or a complex multi-server setup, understanding and correctly setting hostnames can make system organization and communication much better. In this section we’ll go through the steps to manage hostnames in Ubuntu so you can do it right.

#### Using the UI (Graphical Interface)

To set the hostname using the UI, click on the overview "**Activities**" or press Super (**Windows key**) and type **settings**, then scroll to the bottom of the Settings window and click **About**.

On the About window, click the **Device Name box**, type your preferred **hostname**, and click **Rename** to save the changes.

/home/chiloba/Pictures/productivity%20Folder/Productivity-in-Everyday-Use.png

For this case, the hostname was set to cloudspinx.com; change it accordingly and log out of the system and log back in in order to reflect across all sessions.

#### Using the CLI (Command Line Interface)

Advanced users or servers prefer the CLI because it is more flexible. First, open your terminal by pressing Ctrl+Alt+T.

Ubuntu includes the hostnamectl command as part of systemd, which allows you to manage your system's hostname. With this command, you can easily view and change the hostname along with its related settings.

To learn more about how to use the hostnamectl command, you can access the help guide by running the command given:

```bash
hostnamectl --help
```

This command shows a brief help text that outlines the options and commands available for hostnamectl.

- **status** – Display the current hostname along with relevant details.

- **set-hostname** – Modify the system's hostname.

- **set-icon-name** – Give a symbolic name to the host.

- **set-chassis** – Specify the type of machine (e.g., desktop, server).

- **set-deployment** – Indicate the deployment environment (e.g., development, production).

Another way to access the hostnamectl manual page is to execute:

```bash
man hostnamectl
```

The functionality and usage of hostnamectl will be thoroughly explained in this extensive documentation.

Check the current hostname using:

```bash
hostnamectl
```

#### Changing the Hostname

To set the hostname, run the hostnamectl command with the set-hostname option; replace the **new-hostname** in the below command with the desired hostname.

```bash
sudo hostnamectl set-hostname new-hostname
```

    For instance, to set the hostname to be cloudspinx.com, run the below line.

```bash
sudo hostnamectl set-hostname cloudspinx.com
```

Verify the set hostname using the hostnamectl command:

```bash
hostnamectl 
```

The new hostname should reflect in the output:

```bash
 Static hostname: cloudspinx.com
       Icon name: computer-laptop
         Chassis: laptop
      Machine ID: 9b780f5f125f43ffb7a0702c75ae2262
         Boot ID: b638af2c9a5b4a7b83923193b6c1a8c5
```

#### Updating the Hosts File

After changing the hostname, you need to update ''/etc/hosts" to keep the system working properly. This step ensures the hostname is resolved locally so applications and services don’t break.

In this step you will map the new hostname to the loopback IP in /etc/hosts. This will allow your system to resolve its own hostname.

**Editing the Hosts File:**

To edit **/etc/hosts** you will need a text editor. Ubuntu comes with **nano** pre-installed which is user friendly. If you prefer to use **vim** you can install it with the following command:

```bash
sudo apt update && sudo apt install vim
```

To edit the host file with nano, execute:

```bash
sudo nano /etc/hosts
```

Replace the old hostname with the new one in the file.

```bash
127.0.0.1       localhost
127.0.1.1       cloudspinx.com
```

After updating the hostname, you can save and exit the editor by pressing <u>Ctrl+O</u> to save your changes and "Ctrl+X" to exit the editor.

These steps have successfully changed the system hostname and confirmed that it is correctly configured in your Ubuntu environment. This process illustrates how even minor adjustments can significantly improve the overall performance and productivity of your Linux system.

### Configure Time

The following describes how to configure the system timezone in Ubuntu using the CLI (Command Line Interface) and the UI (Graphical Interface):

#### Using the UI (Graphical Interface)

To configure the timezone using the UI, select the **Activities** overview by clicking on it, or search for Settings by pressing the Super key (Windows key). Once you're there, scroll down to the Settings menu, then pick **Date & Time** from the sidebar.

Now turn off  "Automatic Time Zone." Choose your preferred location by clicking on the "Time Zone" field and select from the map.

<img title="" src="file:///home/chiloba/Pictures/productivity Folder/Productivity-In-Everyday-Use.png" alt="" width="631">

In our instance, we selected ``America/Los_Angeles``. At this point, the system will now use the chosen location.

#### **Using the CLI (Command Line Interface)**

For servers or advanced users who prefer to work directly with commands, the CLI is more appropriate for configuring the timezone. You can open the terminal by pressing Ctrl+Alt+T and then run the command below to check the current timezone.

```bash
timedatectl
```

Information like the current timezone, system clock status, and NTP synchronization will be shown in the output.

```bash
  Local time: Tue 2025-01-07 14:06:49 PST
           Universal time: Tue 2025-01-07 22:06:49 UTC
                 RTC time: Tue 2025-01-07 22:06:49
                Time zone: America/Los_Angeles (PST, -0800)
System clock synchronized: yes
              NTP service: active
          RTC in local TZ: no
```

 To view the available time zone names, enter the following command:

```bash
timedatectl list-timezones
```

After running the above command, you'll get an extensive list of the time zones. We can now change the **region/city** in the command below to establish your preferred time zone.

```bash
sudo timedatectl set-timezone Region/City
```

As an alternative, you can combine the ''timedatectl" and **grep** commands to narrow down the search by city name. For example, to search Nairobi, the command will look like below. Replace Los_Angeles with your desired city; hence, press **CTRL + C** to exit.s

```bash
timedatectl list-timezones | grep Los_Angeles
```

**Note**: In a file or text stream, the grep command is utilized to search for a specific pattern or string. It returns lines that match the given pattern.

For instance, we can set the timezone to **America/Los_Angeles**.

```bash
sudo timedatectl set-timezone America/Los_Angeles
```

 After replacing the timezone in the above command, use the **timedatectl** command to confirm the changed timezone; the intended result should look like this.

```bash
   Local time: Tue 2025-01-07 14:06:49 PST
           Universal time: Tue 2025-01-07 22:06:49 UTC
                 RTC time: Tue 2025-01-07 22:06:49
                Time zone: America/Los_Angeles (PST, -0800)
System clock synchronized: yes
              NTP service: active
          RTC in local TZ: no
```

#### Set Universal Time (UTC)

To synchronize time on servers of different time zones, set the time to Coordinated Universal Time (UTC). This approach will be very useful for working in containerized and cloud computing environments because it reduces many complexities brought about by local time changes, including daylight saving. To sync your system with UTC, run the command:

```bash
timedatectl set-timezone UTC
```

Although there is no direct output, *timedatectl* allows the user to check the applied configurations.

```bash
timedatectl
```

With a `+0000` offset, the time zone is clearly set to UTC.

```bash
Local time: Tue 2025-01-07 14:06:49 PST
           Universal time: Tue 2025-01-07 22:06:49 UTC
                 RTC time: Tue 2025-01-07 22:06:49
                Time zone: America/Los_Angeles (UTC, +0000)
System clock synchronized: yes
              NTP service: active
          RTC in local TZ: no
```

The timezone configuration process using the UI and CLI is complete.

### Configure Date

To set the system date in Ubuntu, you can use both the UI (Graphical Interface) and the CLI (Command Line Interface). Follow the steps below to see how to go about each.

#### Using the UI (Graphical Interface)

First, press the Super key (Windows key) and choose Settings to set the system date in Ubuntu. Go to System in the settings menu, then locate **Date and Time**. Once there, disable "Automatic Date & Time" so that manual adjustments can be made.

Click the **date field**, then use the calendar widget to choose the desired date.

![](/home/chiloba/Pictures/productivity%20Folder/Productivity-in-Everyday-Use-23.png)

The selected date will be quickly saved and applied when you've specified it.

#### **Using the CLI (Command Line Interface)**

Setting the date using CLI is the easiest way since you'll only run commands on your terminal. A new date can be established by using the ``date`` command. 

To view the current date, run the date command without options.

```bash
date
```

With this command, the current system time and date will be shown in the following format:

```bash
Tue Jan  7 02:04:40 PM PST 2025
```

Here is the basic format to set the date:

```bash
sudo date -s "YYYY-MM-DD"
```

Here are the parts of the command:

- **-s**: Indicates that the date is being manually "set."  

- **"YYYY-MM-DD"**: The format of the date:  

- **YYYY**: a four-digit year, like 2025.  

- **MM:** Two-digit month (January is 01, December is 12).  

- **DD**: two-digit day (01–31, for example).

For example, to set the date to Feb 01, 2025, you'll type:

```bash
sudo date -s "2025-02-01"
```

Once the command has been executed, verify the modification using:

```bash
date
```

To make sure your changes are permanent, remember to update the "hardware clock" after adjusting the system date.

```bash
sudo hwclock --systohc
```

Explanation of the command:

- **hwclock**: This is the hardware clock, also known as the Real-Time Clock (RTC). It's a battery-powered clock on your motherboard that continues to keep time even when the system is turned off.

- **--systohc**: This means "system to hardware clock.'' It updates the hardware clock to the system clock.

Notes:

- Changing the date can affect system services like scheduled tasks and certificates.

- Use the correct date format.

- After you set the date, check it with the date command.

That's all on how to configure dates using both UI and CLI.

### Configure NTP configurations

In this section, we will look at how to install and configure Chrony and NTP. Computer system clocks can be automatically synchronized via a network thanks to the Network Time Protocol (NTP). The machine can utilize Coordinated Universal Time (UTC) as its system clock instead of local time.  

Accurate timekeeping is crucial in Linux systems, particularly servers, for a number of reasons. For instance, precise timekeeping is necessary in a networked context in order to obtain accurate timestamps in system logs and packets for root-cause analysis, fault occurrence identification, and correlation identification.  
Two popular time synchronization management programs with robust functionality to maintain the accuracy of your system clock are NTP (Network Time Protocol) and Chrony.

#### Installing Chrony

By default, the chrony command is not installed. To install it, run the command given below:

```bash
sudo apt install chrony
```

By default, the command line application is installed at ``/usr/bin/chronyc``, and the chrony daemon is installed at ``/usr/sbin/chronyd``.

The Chrony service must then be started and enabled to launch at system startup.

```bash
sudo systemctl enable --now chronyd
systemctl status chronyd
```

The chronyc command below can now be used to verify if chrony is up and running correctly and to see how many peers and servers are connected to it.

```bash
chronyc activity
```

The result  after above command demonstrates the proper operation of the time synchronization mechanism.

Use the following command to view information about the time sources Chronyd is now querying, such as the list of available servers, their status, and offsets from the source and the local clock. The context for every column is shown with the **-v** flag.

```bash
chronyc sources -v
```

To check **chrony** tracking, execute the command below:

```bash
chronyc tracking
```

The reference ID from the output of this command shows the name (or IP address, if available) of the server that the computer is currently synced with, among all the available servers.

The output offers comprehensive details regarding the state of system clock synchronization.

#### Configuring Chrony Time Sources

A pool of servers or a few default servers ought to be included in your system when you install a Linux operating system in the cloud. To add or change the default servers, edit the configuration file given below:

```bash
sudo nano /etc/chrony/chrony.conf
```

The server directive highlighted in the screenshot can be used to add or modify several servers; ensure that it is displayed in the file.

![](/home/chiloba/Pictures/productivity%20Folder/productivity-in-everyday-use-3.png)

If the server cannot be reached, the system can send a burst of packets using the **iburst** option.

Although these servers are a part of the Ubuntu pool, you have the option to select additional public NTP servers that are located nearer to you here at [ntppool.org.](https://www.ntppool.org/en/ "NTP Pool Servers")

The file has numerous other configuration options. Once the modifications have been made, restart the chrony service.

```bash
sudo systemctl restart chrony
```

Use the timedatectl command to see the current time on your computer, verify that NTP is operational, and see if the system clock is synchronized:

```bash
timedatectl
```

Anticipated results from the command.

```bash
Local time: Wed 2025-01-08 06:47:08 PST
           Universal time: Wed 2025-01-08 14:47:08 UTC
                 RTC time: Wed 2025-01-08 14:47:08
                Time zone: America/Los_Angeles (PST, -0800)
System clock synchronized: yes
              NTP service: active
          RTC in local TZ: no
```

Based on the above output, the system is configured to synchronize time with an NTP server.

#### Install NTP (Optional)

Setting up and configuring NTP is not necessary if you decide to install and configure <u>**Chrony**</u>, and vice versa. If you choose to setup NTP, use Ubuntu's built-in system packages to install the NTP protocol by running the following command.

```bash
sudo apt install ntp 
```

The NTP server must be configured after installation. The location of the NTP configuration file is ``/etc/ntp.conf``. Open with any editor of your choice.

```bash
sudo nano /etc/ntp.conf
```

Once you have opened the configuration file, you can add or modify the server lines from the screenshot to specify your preferred NTP servers.

![](/home/chiloba/Pictures/productivity%20Folder/productivity-in-everyday-use-4.png)

In broad terms, it is preferable to substitute server pools from your own country, or at the very least, your own continent, for these lines. The lower the latency between you and a time server, the better. To identify the nearest NTP server pool to your location, visit the [NTP Pool Project]() website.

![](/home/chiloba/Pictures/productivity%20Folder/Productivity-In-Everyday-Use-5.png)

All you have to do is add the lines to your configuration file after you've located the most pertinent zone. For instance:

```bash
server 0.europe.pool.ntp.org
server 1.europe.pool.ntp.org
server 2.europe.pool.ntp.org
server 3.europe.pool.ntp.org
```

Once you make any change, you've got to restart the NTP service and check the status.

```bash
sudo systemctl restart ntp
systemctl status ntp
```

NTP service should be active and running now.

#### Configure NTP Sync with timedatectl

Let's configure NTP sync with timedatectl using the  following steps. But first, you've  got to verify the status of systemd-timesyncd.

```bash
systemctl status systemd-timesyncd
```

If not installed, you may need to install it with the below command. Once done with installation, start and enable.

```bash
sudo apt install systemd-timesyncd -y 
 systemctl enable --now systemd-timesyncd
```

Lastly, enable NTP time synchronization and verify.

```bash
sudo timedatectl set-ntp true
timedatectl status
```

The system clock synchronized should be **yes**, and the NTP service should be **active**.

## **Adding users into the system**

This section outlines the steps for adding user accounts to a system, customizing user shells, and enabling features such as passwordless sudo. It will also discuss how to configure user environments for Oh My Bash and Oh My Zsh.

### Using the GUI (Graphical User Interface)

GNOME settings provide an interactive method for adding users (standard, administrator, with or without a password). 

- Open settings and go to the **Users** tab.

- Click the ****unlock**** button the user management section by typing the password.

- Click on the “**Add User**” button.

- You can enter the full name, username, administrator or standard account type, and password. If you don't want to set a password, the user will be prompted to enter the password at their initial login.

- Once done, click the **Add** button.

![](/home/chiloba/Pictures/productivity%20Folder/Productivity-In-Everyday-Use-1.png)

The process cannot be finished without user authentication, type your password to the prompt. After finishing the task, the user can then show up in the list of active users.

### Using the Command-Line Interface (CLI)

Let's now discuss how to add a user account on an Ubuntu system using the CLI. In this section we shall see two commonly used options on how to get started using the **adduser** and **useradd** commands.

- Option 1: Using adduser (User-Friendly)

- Option 2: Using useradd (Low-Level Command)

#### Option 1: Using adduser (User-Friendly)

The adduser command builds on the useradd command. Fortunately, it has more capabilities (other than adding the user) and is easier to use than the useradd command. 

**Commonly used options for** `adduser`:

- **`--disabled-password`**: Create a user account without password, that is, without allowing the user to log in with a password.

- **`--gecos`**: Sets the full name and other information of the user.

- **`--home`**: Set a unique home directory.

- **`--ingroup`**: Adds the user to a group.

- **`--shell`**: Sets the default shell for the user.

- **`--no-create-home`**: Avoid giving the new user a home directory.

- **`--quiet`**:  Convenient for scripting, as it filters the majority of the output.

Let's look at its syntax to figure out how it works and what it's used for.

**For Normal User:**

Syntax:

```bash
sudo adduser <Options> <username>
```

**For System Users:**

```bash
sudo adduser --system <Options> <username>
```

Use the **--help** flag as follows for more thorough usage: Type `adduser --help`.

![](/home/chiloba/Pictures/productivity%20Folder/Productivity-In-Everyday-Use-2.png)

Let's talk about some instances and use cases for it.

**Example 1: Create a User With Default Parameters**

For **Regular User:**

```bash
sudo adduser cloudspinx
```

The **adduser** command prompts you to enter the new user's "password," "home directory," "full name," "phone number," and other information in a single line. Input the details as per your desire.

For **System User:**

```bash
sudo adduser --system cloudspinx1
```

To confirm the aforementioned additions or creations, run:

```bash
sudo tail /etc/passwd
```

**Note:** The **tail** command displays the last part of a file or data stream. By default, it shows the last ten lines of the specified file which is  ``/etc/passwd`` that contains user's account information.

 Regular user and system user that is *cloudspinx* and *cloudspinx1* are successfully added.

```bash
chiloba:x:1000:1000:chiloba,,,:/home/chiloba:/bin/bash
swtpm:x:129:140:virtual TPM software stack,,,:/var/lib/swtpm:/bin/false
libvirt-qemu:x:64055:109:Libvirt Qemu,,,:/var/lib/libvirt:/usr/sbin/nologin
libvirt-dnsmasq:x:130:142:Libvirt Dnsmasq,,,:/var/lib/libvirt/dnsmasq:/usr/sbin/nologin
mysql:x:999:1001::/home/mysql:/bin/sh
sshd:x:131:65534::/run/sshd:/usr/sbin/nologin
_chrony:x:132:143:Chrony daemon,,,:/var/lib/chrony:/usr/sbin/nologin
ntp:x:133:144::/nonexistent:/usr/sbin/nologin
cloudspinx:x:1001:1002:c spinx,222,0742356198,0734788223,0723780923:/home/cloudspinx:/bin/bash
cloudspinx1:x:134:65534::/home/cloudspinx1:/usr/sbin/nologin
```

**Note**: The system user that was created with the `adduser` command does not have a login, meaning that a regular user cannot access it. The login shell, however, it is available to the system user that was established with the `useradd` command (and regular users can log into it).

**Example 2: Adding a User with Custom Parameters**

The command given below adds a user with the custom details and arguments, such as:  

- "**--home**": Specifies a different home directory.  

- "**--shell**": Sets a custom shell.  

- "**--uid**": To assign a user-defined UID.

```bash
sudo adduser --home /home/cloudspinx2/ --shell /bin/zsh --uid 1020 linuxuser
```

When you run the above command, you'll be prompted to enter a password, full name, and phone number.  Input it accordingly.

```bash
Adding user `linuxuser' ...
Adding new group `linuxuser' (1020) ...
Adding new user `linuxuser' (1020) with group `linuxuser' ...
useradd: Warning: missing or non-executable shell '/bin/zsh'
Creating home directory `/home/cloudspinx2/' ...
Copying files from `/etc/skel' ...
New password: 
BAD PASSWORD: 
Retype new password: 
passwd: password updated successfully
Changing the user information for linuxuser
Enter the new value, or press ENTER for the default
    Full Name []: J doe
    Room Number []: 334
    Work Phone []: 735678234
    Home Phone []: 72690872
    Other []: 
Is the information correct? [Y/n] y     
```

Features of the `adduser`:  

- Establishes a home directory automatically.  

- sets up the user's files' permissions.  

- Pleasant prompts that make it easier to use.

#### **Option 2: Using useradd (Low-Level Command)**

The **useradd** command creates a new system and regular user. In order to create a user, this command requires the inclusion of additional parameters. With just the following parameters, a user can be added using the useradd command:

- Give each user a home directory and default shell.  

- Uses the group ID (GID) and the potential (next vacant) user ID (UID) to create the user.

Nevertheless, the password and full name are not generated by the useradd command. 

**Commonly used options for** `useradd`:

- **`-m`**: If there isn't a user's home directory existing, it will create.

- **`-s`**: Give the user the default shell.

- **`-d`**: Add the home directory of the user.

- **`-G`**: Make the user a member of more groups.

- **`-p`**: This option is use to set user’s password.

- **`-r`**: Set a system user without a login shell or home directory.

- **`-e`**: Specify the user account's expiration date

- **`-c`**: Create a comment or the user's full name.

- **`-u`**: Set the new user's user ID (UID).

- **`-f`**: Specify how many days will elapse after the password expire before the account is disabled.

Let's start by comprehending the useradd command's syntax:

**Syntax**:

```bash
sudo useradd <options> <username>
```

To see the  list of options that the useradd command supports, run.

```bash
useradd --help
```

Let's utilize this command to generate a new user with a number of features:

**Example 1: User With Default Parameters**

*Regular/Normal User*

With default settings, the command creates a normal/regular user without adding the password, full name, or home directory. *Replace johnspinx with your preferred username*.

```bash
sudo useradd johnspinx
```

We may verify whether the password is set or not using the following superuser (**su**) command (switching to the newly formed user):

```bash
su - johnspinx
```

When switching, make sure to input the user's password. You will not be able to switch to that user if you haven't set it. In this case, set the user's password by executing the following command:

```bash
sudo passwd johnspinx
```

A request to enter a new password will appear. Enter your password again to confirm it.

```bash
New password: 
New password: <Type-new-password>
Retype new password: <Re-type password>
passwd: password updated successfully
```

By entering the user password that was established in the previous stage, you can now switch to that user.

**Example 2: Create a User With a Home Directory**

The `useradd` command does not create the directory by default; it merely allocates it. A user and home directory are created when the useradd command's "**-m**" option is used:

```bash
sudo useradd -m johnspinx2
```

To check if the directory was created:  

- Set the password by using the **sudo passwd** command.   

- Then, to switch to that user, type **su - johnspinx2**. 

- Finally, run the **pwd** command to see the current directory.  

**Note**: Using the ''-**M**'' flag with the useradd command will specifically stop the creation of a home directory for the user.

**Example 3: Create a User With Specific Home Directory**

By using the "**-d**" option, you can add a user with a certain home directory:

```bash
sudo useradd -d <path/to/home/directory> johnspinx3
```

You can select any home directory by entering its path. Replace *spinx* with the directory you want to use.

```bash
sudo useradd -d /home/spinx johnspinx3
```

Confirm the new home directory of the “**johnspinx3** in the ``/etc/passwd`` file together with the ``grep`` command. This file contains the user's account information for the system.

```bash
grep johnspinx3 /etc/passwd
```

The following output shows that the user is successfully addded to the specified home directory.

```bash
johnspinx3:x:1001:1001::/home/spinx:/bin/sh
```

Breakdown of the output:

- **johnspinx3**: The username.

- **x**: Placeholder representing a hashed password stored in /etc/shadow.

- **1001:1001**: User ID (UID) and group ID (GID).

- **/home/spinx**: The designated home directory.

- **/bin/sh**: The default shell for the user.

#### Add User to Sudoers File or Sudo Group

The use of the sudo command to grant administrative rights to users allows access to both the sudoers file and the sudo group.  

The ``/etc/sudoers`` configuration file defines which users or groups are allowed to use sudo for system administration. It specifies which permissions are granted, whether commands must be executed in a password-requiring environment, and more. However, the sudo group was created explicitly for the purpose of handling sudo permissions. Adding users to this group grants them the permission to use sudo, thus allowing them to run commands with superuser privileges.  

Add users to the sudo group using the **usermod** command, in order for them to gain sudo access without changing the sudoers file:

**usermod Linux Syntax:**

```bash
usermod [options] [username]
```

Change the username john to your preferred username.

```bash
sudo usermod -aG sudo john
```

Although there is no output from the command, the **"-aG"** option instructs the system to add the user to the designated group.

The `usermod` command is only one of many commands available to system administrators to manage user accounts. This is used to change any existing user account information, which includes but is not limited to changing the username, password, home directory path, and default shell.

Check the groups that john belongs to in order to confirm they are included in the sudoers group.

```bash
groups john
```

The username and every group to which it belongs are listed 

```bash
john : john sudo
```

**Why is this necessary?**

Users without sudo rights cannot perform tasks that require administrative access, like installing software.

#### **Passwordless Sudo**

Understanding the security implications of using the sudo command without a password is important, even though it can be handy and may save time when working in a Linux environment. If you still want to do it, the following is a step-by-step guide on how to configure sudo to run without asking for a password.

Edit the sudoers configuration file. It is not recommended to use a standard text editor to directly edit the sudoers file. Instead, use the **``visudo``** command:

```bash
sudo visudo
```

Locate the section that appears as follows:

```bash
root    ALL=(ALL:ALL) ALL
```

Here is the format to use: replace **username** "cloudspinx" with your actual username:

![](/home/chiloba/Pictures/productivity%20Folder/Productivity-In-Everyday-use-22.png)

If you want to disable the password prompt only for a single command, replace **ALL** at the end with the full path to that specific command. For example:

```bash
username ALL=(ALL:ALL) NOPASSWD: /path/to/command
```

Save and exit. In case visudo opens with ``Vim`` editor by default as it is in the case of most computers: press **Esc**, then type ``:wq`` followed by Enter. If instead you are using nano type: "Ctrl + O" Enter and "Ctrl + X" at the end.

**Use Case of passwordless sudo:**

It is Suitable for automated scripting, system administration, or development environments.

#### Changing Sudo Password

Administrative commands are carried out using the sudo command, which prompts for the sudo password. This will allow users to temporarily elavate to superuser or root privileges without actually logging in as the root user. Here is how the sudo password can be changed:

The **passwd** command can be used by a superuser to change and update any user's settings. Regular users can only change can only change password. 

To change the password for a specific user, you can use the passwd command with sudo privileges followed by the username of the account you wish to update.

```bash
sudo passwd <username>
```

For example to change password for john, run:

```bash
sudo passwd john
```

The output after running the command will show that the password is updated successfully.

```bash
[sudo] password for john: 
New password: <Type-new-password>
Retype new password: <Re-type password>
passwd: password updated successfully
```

#### Change Sudo Password via GUI

In Ubuntu, you can use the graphical user interface (GUI) to change the sudo password without needing to use the terminal or any commands. Just follow these steps:

- Open the **settings** in the overview activities. 

- Navigate to the **Users** after lauching settings app.

- Select the user you want to update it's password.

- After selecting the user, click the **password** field.

- A new Change Password pop-up window appears. Enter your **old sudo** password and your **new one**, then **retype the new** password to confirm it.

- Once you've completed filling the fields, click the **Change** button to verify the changes.

![](/home/chiloba/Pictures/productivity%20Folder/Productivity-in-Everyday-Use-21.png)

Following the aforementioned procedures, you will be able to change your sudo password using both the UI and the CLI.

#### Setting Shell

The bash shell is among the most used login shells with Linux. However, some of the functions of using the command line have some alternatives. Users can employ the ``chsh`` or *change shell* command in changing the login shell in Linux.

**chsh command Syntax:**

```bash
chsh [Options] [Shell] [Username]
```

When chsh is used on its own, it allows the active user to change their shell.

```bash
chsh
```

When you run the command chsh, the terminal will ask for the current user's password. After that, it prompts the user to choose a new shell. If you prefer to keep the default shell, simply press **Enter**.

```bash
Password: 
Changing the login shell for chiloba
Enter the new value, or press ENTER for the default
    Login Shell [/bin/bash]: 
```

The options alter the command's output. Although it is optional, the command asks you to input a shell if the [**shell**] argument is left empty.

`Chsh` options for customizing outputs:

- -**l**: Specifies the user's login shell.

- -**u**: Shows the available shells list.

- -**s**: Assigns the specified shell as the user's login shell. 

- -**r:** Directory to chroot into.

- -**v**: Prints details about the chsh version and exits.

- -**h**: Displays help text and exits.

To check the available list of shell, you'll run the **cat** command with **/etc/shells.**

```bash
cat /etc/shells
```

Upon execution, the command will output multiple shells.

**Cat**, short for concatenate, is one of those Linux/Unix command line tools which is utilised pretty frequently to read, view as well as combine the content of the files. 

#### Change Login Shell

Use the **-s** option with chsh to change the current user's shell for instance to **/usr/bin/tmux**.

```bash
chsh -s /usr/bin/tmux
```

There is no output from the command. Run **chsh** without any arguments to verify the change:

```bash
chsh
```

The result below will indicate that /usr/bin/tmux is the shell.

```bash
Password: 
Changing the login shell for chiloba
Enter the new value, or press ENTER for the default
    Login Shell [/usr/bin/tmux]: 
```

The modification is verified by the value in square brackets, which is `/usr/bin/tmux`.

**Specifying the Shell During User Creation**

You can also specify the shell directly when you create the user with the `-s` option and then the full path to the shell you want for example, `/usr/bin/zsh` for `zsh`. 

Here is a usage example: Replace the "username" with the actual username.

```bash
sudo useradd -m -s /usr/bin/zsh username
```

-  `-m`:  This option will creates the user's home directory if it does not exist.

If you have already created a user and you would like to set the user's shell to `zsh`, you would do so using the *chsh* command:

```bash
sudo chsh -s /usr/bin/zsh username
```

#### Changing Login Shell for Another User

Setting a new login shell for another user can be accomplished by the root user or any user with sudo privileges by providing the username as an input.

As an example, alter john default shell using:

```bash
sudo chsh john
```

Enter the path to select the new shell. The chosen shell in this instance is `/bin/sh`:

```bash
Changing the login shell for john
Enter the new value, or press ENTER for the default
    Login Shell [/bin/bash]: /bin/sh
```

To confirm the modification, login to john using the superuser command (su) and run "chsh".

```bash
su john
chsh
```

The output should show **/bin/sh** as the new shell.

```bash
Password: 
Changing the login shell for john
Enter the new value, or press ENTER for the default
    Login Shell [/bin/sh]: 
```

Th e above output shows that the shell for john was changed to /bin/sh.

#### Change Shell Without User Interaction

`chsh` is interactive by default and asks the user for the new shell. However, the shell is changed non-interactively by **-s** option. Example: Change the login shell of the current user to ``/bin/sh``:

```bash
chsh -s /bin/sh
```

There is no output from this command. However, **chsh -s** changes the shell without needing any further input from the user. You can use **chsh** to verify the change.

It is also possible to change the shell for another user without any input by using the **-s** parameter. You need to have root or sudo level powers to run this command. 

Syntax:

```bash
chsh -s [Shell] [Username]
```

To illustrate, set john shell to ``/bin/rbash`` run:

```bash
sudo chsh -s /bin/rbash john
```

The below output shows that John shell is set to /bin/rbash.

```bash
Password: 
Changing the login shell for john
Enter the new value, or press ENTER for the default
    Login Shell [/bin/rbash]:
```

#### Customizing the User Shell Environment

**Why Customize the Shell?**

- **Productivity**: Utilize plugins, shortcuts, and aliases to speed up repetitive tasks.

- **Aesthetics**: The command line interface can be visually appealing with various themes.

- **Personalization**: Allow the environment to be tailored to the user's preferences.

##### Install and Customize Oh My Bash

Manage and customize the Bash shell with Oh My Bash, an open-source framework. It enhances your experience at the terminal by including:

- Predefined themes.

- Plugins to enhance functionality.

- Configurations and aliases for efficiency.

Let's now focus on the installation and customization of Oh My Bash.

1. **Install Git**

First we need to install Git which is necessary when obtaining Oh My Bash from its GitHub repository. Run the commands below to install it.

```bash
sudo apt update && sudo apt install git -y
```

2. **Install Oh My Bash**

The Installation script for Oh My Bash is found on GitHub. To install it, download the script using either `curl` or `wget`.

If curl or wget is not installed, run the command below to install it.

```bash
sudo apt install curl wget
```

- Via wget.

```bash
bash -c "$(wget https://raw.githubusercontent.com/ohmybash/oh-my-bash/master/tools/install.sh -O -)"
```

- Via curl.

```bash
bash -c "$(curl -fsSL https://raw.githubusercontent.com/ohmybash/oh-my-bash/master/tools/install.sh)
```

After a successful download, you should see the below in the screenshot.

![](/home/chiloba/Pictures/productivity%20Folder/Productivity-in-Everyday-Use-20.png)

Explanation of the above command:

- **bash -c**:  executes the provided script.

- **curl -fsSL**: uses the URL to download the script.

This script will do the following when run: It will install Oh My Bash into **~/.oh-my-bash/** and back up your existing **.bashrc** file into **.bashrc.omb-backup**. It will then configure your .bashrc with Oh My Bash settings.

After installation, the default Oh My Bash theme will be displayed in your terminal prompt. To verify:

```bash
echo $OSH
```

Oh-my-bash should be the default output once the command has been executed.

```bash
/home/john/.oh-my-bash
```

Installation is successful if the output shows the path to "~/.oh-my-bash".

##### Customize Oh My Bash

**Change the Theme**

Themes change the look of your terminal prompt. You can also change the list of the available themes, which is located under **~/.oh-my-bash/themes/**. To list this theme's run:

```bash
ls ~/.oh-my-bash/themes/
```

To set the new theme, open the **.bashrc** file using a text editor such as nano, which is installed by default on Ubuntu.

```bash
nano ~/.bashrc
```

Locate the below line and replace the **font** in the command below with your favorite theme.

```bash
OSH_THEME="font"
```

For this case, we shall use the **agnoster** theme.

![](/home/chiloba/Pictures/productivity%20Folder/Productivity-in-everyday-Use-10.png)

Save and exit the file by typing `Ctrl+O` to save and `Ctrl+X` to exit. 

Lastly, reload the file by running the command below:

```bash
source ~/.bashrc
```

**Tip**: Explore the themes and find the one that fits the best for you! You can simply refer [more themes.](https://github.com/ohmybash/oh-my-bash/wiki/Themes)

**Adding  Plugins**

Plugins bring some very useful features to your shell, like autocompletion and Git shortcuts. Some plugins, such as **Git**, are enabled by default.

To enable additional plugins on Oh My Bash, open the ".bashrc" file by running:

```bash
nano ~/.bashrc
```

Find the line below in the file:

```bash
plugins=(git)
```

To add more plugins, you have to separate each with spaces. Replace the below line with your desired plugins. Check the below instance.

![](/home/chiloba/Pictures/productivity%20Folder/Productivity-in-Everyday-Use-19.png)

Reload the shell to make changes in the environment.

```bash
source ~/.bashrc
```

You can check [more plugins](https://github.com/ohmybash/oh-my-bash/wiki/Themes).

**Customize Aliases**

Aliases allow you to have shortcuts for commands. To create an alias, open the file below.

```bash
nano ~/.bashrc
```

Add the below line at the bottom of the file. Check the below example and replace it with your preferred aliases. 

```bash
alias untar='tar -xvf'          # Extract tar files easily
alias zipf='zip -r'             # Create zip archives recursivelylias ll='ls -alF'
alias gs='git status'           # Shortcut for git status
alias ga='git add .'            # Add all changes
alias gc='git commit -m'        # Commit with a message
alias gp='git push'             # Push to remote repository
alias update='sudo apt update && sudo apt upgrade -y'
alias install='sudo apt install'                      # Shortcut for package installation
```

Save the file and reload the file for changes to take place.

```bash
source ~/.bashrc
```

##### Install and Customize Oh My Zsh

Oh My Zsh is a powerful open-source framework designed to manage and customize the Zsh shell. It enhances your terminal with functionalities such as:

- Syntax highlighting and automated suggestions.

- Highly customizable themes.

- Code generation plugins (such as Git integration and Docker umuge)

Before installing Oh My Zsh, ensure that you've already installed Git since you'll be using it to download Oh My Zsh from GitHub. If not installed, run the below commands to accomplish it.

```bash
sudo apt update && sudo apt install git -y
```

**Install Zsh**

Check if Zsh is installed by running the command below to check the version.

```bash
zsh --version
```

If Zsh is not found, you can install it using:

```bash
sudo apt install zsh -y
```

Zsh will be set as the default for the current user. You can as well verify using:

```bash
chsh -s $(which zsh)
```

Zsh will be set default for the current user. You can as well verify using:

```bash
zsh
```

The output below demonstrates that zsh is configured by default.

```bash
password: 
Changing the login shell for chiloba
Enter the new value, or press ENTER for the default
    Login Shell [/usr/bin/zsh]:
```

**Install Oh My Zsh**

To install Oh My Zsh, you can use either curl or wget to execute the installation script.

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

By running the aforementioned command, Zsh will become the user's default shell. There is no need to restart the server or log off. To start the procedure, just type "**Y**" and hit "**Enter**." It will finish in a matter of seconds. The output that appears in your terminal window should be as follows:

![](/home/chiloba/Pictures/productivity%20Folder/Productivity-in-Everyday-Use-17.png)

Explanation:

- **sh -c:** executes the script that it downloaded.

- The script creates a **.zshrc** for the customizations and also installs Oh My Zsh in the **~/.oh-my-zsh/** directory.

Verify Installation: Upon installation, you would notice the default Oh My Zsh theme (Robbyrussell) right in your terminal prompt. To confirm:

```bash
echo $ZSH
```

Installation was successful if you see the path of "~/.oh-my-zsh" displayed.

**Change the Theme**

The look of your terminal prompt is customizable with themes. And these themes are stored in the `~/.oh-my-zsh/themes/` You can list the available themes using:

```bash
ls ~/.oh-my-zsh/themes/
```

You'll get an extensive list of themes when you run the aforementioned command. Alternatively, you can open the link below in your browser and choose your best theme.

```bash
https://github.com/ohmyzsh/ohmyzsh/wiki/Themes 
```

Set the new theme by opening the **.zshrc** file with your favorite editor.

```bash
nano ~/.zshrc
```

Locate the below line and replace robbyrussell with your best theme. 

```bash
ZSH_THEME="robbyrussell"
```

For this case we will choose <u>amuse</u>.

![](/home/chiloba/Pictures/productivity%20Folder/Productivity-in-Everyday-Use-15.png)

Once you've changed the theme, save the file and reload the environment.

```bash
source ~/.zshrc
```

**Configure the Auto-Suggestions Plugin**

By enabling and configuring the auto-suggestions plugin, you will be able to automatically and periodically receive command suggestions according to your Zsh command history, saving time and allowing you to complete daily tasks much easier—the more frequent the commands are, the easier! To enable auto-suggestions, follow the steps mentioned below:

First, you have to add the auto-suggestion plugin repository. This can be done by cloning the repository:

```bash
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

Edit the .zshrc file with the editor of your choice. You can simply use the default one, which is nano.

```bash
nano ~/.zshrc
```

 Add the auto-suggest plugin to the plugins section of the file by inserting it into the array of plugins, like this:

![](/home/chiloba/Pictures/productivity%20Folder/Productivity-in-Everyday-Use-14.png)

Save and exit the editor; hence, reload the file for modifications to take place.

```bash
source ~/.zshrc
```

Now, you can accept the recommendation and easily finish the command by using the "right arrow" key when typing it.

**Enable Syntax Highlighting**

The syntax highlighting brings some benefits, such as making the code more readable, the errors easier to spot, programming language recognition, better productivity, and a nicer-looking interface. Here is how to add syntax highlighting to Zsh:

Use the command below to clone the plugin repository:

```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

Once the plugin repo is repo is done, open the ".zshrc" file: 

```bash
nano ~/.zshrc
```

Proceed to the plugins area and add **zsh-syntax-highlighting** to the plugin list, separating with space.

![](/home/chiloba/Pictures/productivity%20Folder/Productivity-in-Everyday-Use-12.png)

Save and exit the file. Also, you've got to reload your terminal for Zsh to activate syntax highlighting.

```bash
source ~/.zshrc
```

For example, if you type a command incorrectly, it will be highlighted in **red**; if you type it correctly, it will be displayed in **green**:

![](/home/chiloba/Pictures/productivity%20Folder/Productivity-in-Everyday-Use-11.png)

In the provided example, we used the "**echo**" command to show how highlighting works.

**Customize Aliases**

Aliase will help you to create shortcuts for a given command. To add an alias, open the file below.

```bash
nano ~/.zshrc
```

Let's now add aliases. Navigate to the bottom of the file and add the below lines, for instance, to add Docker aliases.

```bash
alias ll='ls -lah --color=auto'  # Detailed list with human-readable sizes
alias ..='cd ..'                # Move up one directory
alias ...='cd ../..'            # Move up two directories
alias df='df -h'                # Display disk usage in human-readable format
alias du='du -h --max-depth=1'  # Show size of directories in human-readable format
alias f='find . -name'          # Simplified file search
alias grep='grep --color=auto'  # Highlight matches in grep output
alias psu='ps aux | grep'       # Quickly find processes by name
alias free='free -m -t'         # Show memory usage in MB
alias cls='clear'               # Clear terminal screen
alias h='history'               # Show command history
```

Save and exit the file and lastly refresh the shell. 

```bash
source ~/.zshrc
```

**Enhanced History Search**

Reverse history search is normally accessed by pressing **CTRL + R**. You can use it to look up any word in your command string in your command history. To locate the final command using the substring `oh-my`, press "CTRL + R" and type it:

![](/home/chiloba/Pictures/productivity%20Folder/Productivity-in-Everyday-Use-9.png)

To go back in history, keep pressing "CTRL + R." To go forward, use "CTRL + S."

Zsh enhances this feature by allowing you to filter your command history. If you start typing a command, you can use the **UP** and **DOWN** keys to navigate through the history that matches your input. For instance, if you type "apt" and press **UP**, you'll see the most recent command that begins with that substring.

**Dirhistory plugin**

Recall your past directory access history. This plugin makes it easier to use your directories. It has keyboard bindings to navigate through directory history. First, add dirhisotry to the configuration file:

```bash
nano ~/.zshrc
```

Navigate to the plugin section and add dirhistory.

```bash
plugins=(… dirhistory)
```

Save the file and restart the zsh setup.

```bash
source ~/.zshrc
```

One may now navigate through the history of their directory by utilizing the key bindings provided below:

- Press **ALT + LEFT** to access the previous directory.  

- Press **ALT + RIGHT** to navigate to the next directory.  

- Press **ALT + UP** to navigate to the parent directory.  

- Use **ALT + DOWN** to navigate to the first child directory.

**History Timestamps**

Every history command will include a time stamp, which is quite useful. To enable this feature, simply uncomment the line in the `~/.zshrc` file and choose your desired date format.

```bash
HIST_STAMPS="mm-dd-yyyy"
```

For this case, the format will look like below:

```bash
 HIST_STAMPS="12/20/2024"
```

Save and exit the file; hence, refresh it using `source ~/.zshrc`. By doing this, a timestamp will appear next to each command that the history command displays.

```bash
history
```

After running history command, timestamp will appear like as shown in the output.

```bash
12   12/20/2024  source ~/.zshrc\n
13   12/20/2024  echo $SHELL
14   12/20/2024  echi $SHELL
15  12/20/2024  sudo nano ~/.zshrc\n
16   12/20/2024  source ~/.zshrc
17  12/20/2024  history
18  12/20/2024  cd Downloads
```

**Automatic Updates**

You may want to enable automatic updates for Oh My Zsh. Once a new version of Oh My Zsh is available, simply uncomment the line in the "~/.zshrc" to initiate the update:

```bash
zstyle ':omz:update' mode auto
```

**JSON Tools Plugin**

You often need to work with JSON directly in your terminal, especially when testing new API requests, since it is the standard data format for web development. This process is significantly improved by using the JSON Tools Plugin. To test this plugin, update your "~/.zshrc" configuration file:

```bash
plugins=(… jsontools)
```

Your JSON data can now be processed using the appropriate JSON tool. A standard JSON dump, for instance, can be a confusing mess. To illustrate this point, attempt to fetch a list of all dog breeds from the popular Dog API service:

```bash
curl https://dog.ceo/api/breeds/list/all
```

![](/home/chiloba/Pictures/productivity%20Folder/Productivity-in-Everyday-Use-8.png)

Let's use the beautiful print jsontool to <u>pipe</u> this JSON dump for better readability:

```bash
curl https://dog.ceo/api/breeds/list/all | pp_json
```

![](/home/chiloba/Pictures/productivity%20Folder/Productivity-In-Everyday-Use-4.png)

As can be seen, the output is now human-readable. The JSON Tools Plugin makes JSON data in your terminal much more human-readable.

You have the freedom to make adjustments and further customize your Zsh environment. Zsh is a powerful scripting language, allowing you to modify your command line setup in any way you prefer. If you decide to explore this in depth, make sure to consult the [official zsh documentation](https://zsh.sourceforge.io/Doc/Release/zsh_toc.html).

## System Update and Upgrades

After using Ubuntu for a few days or weeks, you might find yourself wondering how to update your system for security patches, bug fixes, and application upgrades, especially if you're new to it.

Ubuntu is quite easy to update. I'm not making this up. It only requires executing two commands:

```bash
sudo apt update && sudo apt upgrade
```

Indeed, updating your Ubuntu system can be done in two different ways:

- Using the CLI (Command Line)

- Utilizing the Software Updater GUI tool

### Method 1: Update Ubuntu via CLI

To start, open the Ubuntu desktop terminal. You can do this by using the keyboard shortcut "Ctrl+Alt+T" or by searching for it in the menu. If you're logged into an Ubuntu server, a terminal should already be accessible to you.

Once you open the terminal, run the below commands:

```bash
sudo apt update && sudo apt upgrade -y
```

**Note**: *There will be a password request. You can use the password you have created for your account. Just keep typing your password in terminal and press Enter because you will not see any characters on the screen. This will update the packages of Ubuntu.*

You see how simple it is to use the terminal to upgrade Ubuntu? Let me now clarify the aforementioned command.

In reality, it is a mixture of two commands rather than a single one. In Linux, the **&&** operator allows you to execute multiple instructions so that the second operation only executes once the first command has completed successfully.

The last "**-y**" automatically enters "**yes**" when the program "<u>apt upgrade</u>" asks for your approval before patching.

It will take a little longer since you have to wait for one command to finish before the entry of the second.

**More than just OS updates**: *Linux, on the other hand, uses a package manager. Everything is updated as soon as you run the updates; all packages are installed through Apt. All apps, if any, are updated by the Ubuntu update, either through the Software Center. Linux kernel, the core, and deb packages or installed via an **apt** command.*

**<u>Explanation: sudo apt update</u>**

It's the command used to update the local package database. If this command isn't run, the system will never know about new versions of packages available, and the local database won't be updated.

You will notice a number of URLs in the output when you run the `sudo apt update `command because it retrieves the package information from the corresponding repositories (the URLs you see in the output).

**List Available Upgrades**

You can see the number of packages that can be upgraded at the end of the command. The command below can be used to view these packages:

```bash
sudo apt list --upgradable
```

**<u>Explanation: sudo apt upgrade</u>**

This program ensures that the local database aligns with the versions of installed packages. Once it collects information on each package, it will show you which ones have newer versions available. You will then have the option to update the installed packages to their latest versions.

You can accept the installation of updates by typing "**yes**," "**y**," or simply pressing *enter*.

The command **sudo apt update** checks for available updates to packages, while **sudo apt upgrade** actually installs those updated packages.

### Method 2: Update Ubuntu via the GUI

You don't need to utilize the terminal if you need to update the Ubuntu system using GUL. Locate "**Software Updater**" in the menu, then launch it.

- It will determine whether your system has any "available updates".

- It will provide you the option to "install any updates" that are available.

- Press the "**Install Now**" button. It might request your password.

![](/home/chiloba/Pictures/productivity%20Folder/Productivity-In-Everyday-Use-8.png)

- The updates will begin to be installed as soon as you enter your password.

- To ensure the installed updates work properly, you may need to **restart** your Ubuntu system from time to time. If a restart is necessary, you will be notified at the end of the update process.

- If you would rather not reboot your system immediately, you can opt to do so later.

Congratulations! As the last window should verify, your Ubuntu system is now up to date. In order to finish the upgrade, the software updater might suggest that you restart your computer.

**Using update-manager-core**

A command-line utility named update-manager-core helps in managing distribution upgrades, like transitioning from old Ubuntu version to a newer release.

You'll need the "update-manager-core" package to oversee the upgrade procedure. With this command, you can add it if it isn't already installed:

```bash
sudo apt install update-manager-core
```

Use the following command to update to the most recent version of Ubuntu after you've installed update-manager-core.

```bash
sudo do-release-upgrade
```

Hold off until the installation is finished. It may take a long time. Once the installation is done, reboot the system.

```bash
sudo reboot
```

Upon restarting your computer, you may confirm that the upgrade was successful.

```bash
lsb_release -a
```

![](/home/chiloba/Pictures/productivity%20Folder/Productivity-In-Everyday-Use-9.png)

There you have it. You now understand how to update Ubuntu to the most recent LTS version.

### **Enable Automatic Updates on Ubuntu**

Ubuntu provides two methods for automatic update setup: one through the "terminal" and another using "GNOME." The terminal offers more control and many more options for configuration. 

To set up automatic updates on Ubuntu using the "terminal," do the following:

**1: Install the unattended-upgrades Package**

Security and other critical updates can be installed automatically without human involvement thanks to the ``unattended-upgrades`` package. Run the following lines to install it.

```bash
sudo apt update
sudo apt install unattended-upgrades
```

You can verify that the service is operational by entering the following command:

```bash
systemctl status unattended-upgrades
```

**Configure the unattended-upgrades**

Once the installation is finished, configure each component separately and specify the auto-update parameters. Use your best editor to edit the following file for configuration.

The configuration file for unattended upgrades is typically found in the directory `/etc/apt/apt.conf.d`.

```bas
sudo nano /etc/apt/apt.conf.d/50unattended-upgrades
```

![](/home/chiloba/Pictures/productivity%20Folder/Productivity-In-Everyday-Use-10.png)

The unattended-upgrades package ignores commented lines that begin with **//**.

The following lines in the configuration must be left uncommented for unattended-upgrades to function properly:  

- **"distro_id:distro_codename"** identifies the primary repository for obtaining updates for the given codename and distribution.

- **"distro_id:distro_codename-security"** identifies the security repository from which important security updates can be obtained.

Since **distro_id** and **distro_codename** are placeholders that are automatically updated with the appropriate values of the distribution and codename of the Ubuntu system where the configuration is applied, there is no need to change them with actual values.

**Blacklist Packages**

Certain packages cause other software components to become unstable or incompatible. Sysadmins can avoid unintentional system stability disturbances caused by automated upgrades by blacklisting these programs.

Users can prohibit upgrades for particular packages in the Unattended-**Upgrade::Package-Blacklist config** file section.

To accomplish this, include the required package name in the list. Don't forget to uncomment the line by removing **//**. **"Nginx"** is being added to the list in this illustration:

![](/home/chiloba/Pictures/productivity%20Folder/Productivity-In-Everyday-Use-11.png)

Save and exit the file.

**Enable Automatic Updates**

Edit the auto-upgrades file with the following command to enable Ubuntu automatic updates:

```bash
sudo nano /etc/apt/apt.conf.d/20auto-upgrades
```

Add or change the following lines to modify the frequency of updates:

```bash
APT::Periodic::Update-Package-Lists "1";
APT::Periodic::Download-Upgradeable-Packages "1";
APT::Periodic::AutocleanInterval "7";
APT::Periodic::Unattended-Upgrade "1";
```

In the above lines, **1** indicates that automatic updates are enabled; if it was set to **0**, it indicates that they are not enabled.

The file allows you to specify how frequently the auto updates occur. The file contains the following lines:  

- **Update-Package-Lists**. Use 1 to activate auto-update.  

- **Unattended-Upgrade**. Type 1 to enable automatic upgrades.  

- **AutocleanInterval**. Allow auto-clean packages for a set number of days. For example, **APT::Periodic::AutocleanInterval** "7"; indicates that the system clears the download archive every "seven" days.

Save and exit the file after modifications. Hence, restart the **unattended-upgrades** service by using the command below.

```bash
sudo systemctl restart unattended-upgrades.service
```

**Setting up Automatic Updates using GUI**

GNOME offers an easy-to-use graphical user interface (GUI) for managing system settings, including automatic updates. To enable automatic updates in GNOME, follow the instructions below:

**Step 1**: **Open the Software & Updates App.**
To open the Software & Updates app, follow these steps:

- On the bottom right, click the **Show Applications** icon.

- Type **Software** & **Updates** in the search box.

- Click the "Software & Updates" button.

**Step 2**: **Turn on automatic updates.**
After you open the Software & Updates app, follow these steps:

- Click the **updates** tab.

- Find the section "when there are security updates".

- Choose the options "**Download**" and "**Automatic installation**."

![](/home/chiloba/Pictures/productivity%20Folder/Productivity-In-Everyday-Use-12.png)

**Setting Up Email Notifications for Ubuntu Updates**

Email notifications give system administrators instant access to Ubuntu updates, keeping them updated on important patches and security enhancements. The procedures below will enable email updates.

First, open the configuration file below with your favorite editor, for instance, "nano."

```bash
sudo nano /etc/apt/apt.conf.d/50unattended-upgrades
```

Go down till you get to the section that begins  "Send email to this address for problems or packages upgrades." There are comments in the section. The lines described in the following step must be uncommented before you can send emails.

![](/home/chiloba/Pictures/productivity%20Folder/Productivity-In-Everyday-Use-13.png)

To activate email alerts, remove the **//** and make the following adjustments:
"unattended-Upgrade::Mail." This line specifies the email address for sending notifications. To ensure that the notifications reach the correct recipient, delete the "//" symbol and input the actual email address.

 In the example below, the line is uncommented, and ckipson@gmail.com is included as the email address:

```bash
Unattended-Upgrade::Mail "ckipson@gmail.com""
```

![](/home/chiloba/Pictures/productivity%20Folder/Productivity-In-Everyday-Use-14.png)

**//Unattended-Upgrade::MailReport "on-change";** This line determines whether emails are sent for all updates, regardless of whether an error occurs, or only when errors happen during the update process.

As an illustration, in the example below, the value is set to "**only-on-error**," and the **//** sign is removed:

```bash
Unattended-Upgrade::MailReport "only-on-error";
```

It should look like below in the screenshot.

![](/home/chiloba/Pictures/productivity%20Folder/Productivity-In-Everyday-Use-15.png)

Once you update the file, save the changes and exit the file.

**NOTE:** To ensure the email notification system works properly, you need to install the mailutils package on your system. If you haven't done so, you can run the command below: 

```bash
sudo apt install mailutils
```

Ubuntu's automated security updates have been successfully installed, set up, and enabled.

#### Configure Proxy Settings on Ubuntu

A proxy server mediates internet access. Companies deploy proxies to introduce an additional level of network security and to protect network communication. They are also deployed by individuals seeking to enhance their online privacy and bypass network restrictions.

We shall look at how to configure proxy on Ubuntu both using GUI and CLI.

##### Setting  Up proxy using GUI

Using the desktop GUI in Ubuntu is a straightforward method of configuring a proxy server. Take the actions listed below:

- Launch the **Settings** menu in Ubuntu

- Choose ***Network->Network proxy*.**

- Choose **Manual** from the "Method" drop-down list, then enter the **IP** address and **port number** of your proxy server.

![](/home/chiloba/Pictures/productivity%20Folder/Productivity-In-Everyday-Use-16.png)

##### Setting Up Proxy using CLI

For more precise proxy setup control, use the terminal. As a result, you can:

- Modify the proxy in a temporary or permanent manner.

- The proxy can be set up for a single user or the entire system.

To create a proxy connection, use this syntax:

```bash
[variable]="[username]:[password]@[proxy_address]:[port_number]"
```

If the username and password are not needed by the proxy, leave them out. These parameters are set by Ubuntu using the environment variables listed below:

- **http_proxy** is a proxy server for HTTP connections.  

- **https_proxy** is a proxy server for HTTPS connections.  

- **ftp_proxy**. A proxy server for FTP connections.  

- **no_proxy**. A comma-separated list of addresses and domains to bypass the proxy (suitable for local addresses or intranet).

Variable names in older systems are all capitalized. Use both uppercase and lowercase variable names to account for all potential outcomes.

**Setting up Temporary Proxy for a Single User**

Upon rebooting the system, a temporary proxy connection is reset. To temporarily set up a proxy for the current user, use the export command.

For instance, use the following three commands to export HTTP and HTTPS proxies on 192.168.10.135 port 8080 without a username or password, ensuring that local traffic ignores the proxy:

```bash
export http_proxy="192.168.10.135:8080"
export https_proxy="192.168.10.135:8080"
export no_proxy="localhost,127.0.0.1,::1"
```

The current session's settings are modified by the commands.

**Setting up Permanent Proxy for a Single User**

The .bashrc file can be edited to make modifications that are permanent for a single user. The steps are as follows:

Open the file below using a text editor such as nano.

```bash
sudo nano ~/.bashrc
```

After opening .bashrc file, add the export commands at the bottom. Check the example:

```bash
export http_proxy="192.168.10.135:8080"
export https_proxy="192.168.10.135:8080"
export no_proxy="localhost,127.0.0.1,::1"
```

![](/home/chiloba/Pictures/productivity%20Folder/Productivity-In-Everyday-Use-17.png)

Save and exit the file. Once you save the file, apply the updated configurations to the active session using the command below.

```bash
source ~/.bashrc
```

By running the .bashrc file, the command will implements the modified configurations.

**Setting up Permanent Proxy for All Users**

Modify the `/etc/environment` file with a text editor to permanently enable proxy access for every user:

```bash
sudo nano /etc/environment
```

Add the proxy information to the file. For instance:

```bash
export http_proxy="192.168.10.135:8080"
export https_proxy="192.168.10.135:8080"
export no_proxy="localhost,127.0.0.1,::1"
```

Change the variables to uppercase when running on an older system, or add them below the lowercase variables.

After you save the file and log out, the modifications take effect when you log in again.

#### **Configure APT to Use HTTP and HTTPS Proxy**

Since the Ubuntu repository (apt command-line program) does not use system environment variables, it requires a separate proxy configuration on some Linux-based computers. The methods for configuring it are listed below.

To configure the proxy settings for **apt**, create or modify the **apt.conf** file in the **/etc/apt** directory, if one already exists.

```bash
sudo nano /etc/apt/apt.conf
```

In your /etc/apt/apt.conf file, add this line (replace your proxyaddress and proxyport with your own information).

```bash
Acquire::http::Proxy "http://yourproxyaddress:proxyport/";
Acquire::https::Proxy "https://yourproxyaddress:proxyport/";
```

For instance:

```bash
Acquire::http::Proxy "http://192.168.10.135:8080/";
Acquire::https::Proxy "https://192.168.10.135:8080/";
```

Save and exit the file.

If your proxy requires a password or login subtitute: `http://yourproxyaddress:proxyport` 

 With:

`http://username:password@yourproxyaddress:proxyport`.

```bash
Acquire::http::Proxy "http://username:password@yourproxyaddress:proxyport/";
Acquire::https::Proxy "https://username:password@yourproxyaddress:proxyport/";
```

Remember to substitute the correct **proxy IP address/username** and **port** for proxy_server and port from the aforementioned examples. You will need to restart the system in order to apply the updated configuration.

```bash
sudo reboot
```

**How to Check Whether Ubuntu Proxy Works**

The way the Ubuntu proxy was originally configured determines how to check if it is functioning. GUI users can check the proxy settings to make sure they are enabled and correct.  

Another option is to verify the proper setting using the terminal:

- **Environment variables**: Use the **echo** command to verify that the environment variables are set:

The "echo" command provides a flexible way to print variables and text.

```bash
echo $http_proxy
echo $https_proxy
```

- **APT**: To check the APT proxy, perform an update:
  
  ```bash
  sudo apt update
  ```

## Office Suite

An office suite is a collection of applications designed to increase productivity. It provides everything one needs to create documents, manage data, design presentations, and more. These suites are very important in both personal and professional environments since they enable users to handle word processing, spreadsheets, and slideshows efficiently.  

In the contemporary (modern) landscape, several free and open-source office suites provide robust alternatives to proprietary software; they offer extensive functionality without necessitating expensive subscriptions. **FreeOffice, OnlyOffice, Apache OpenOffice, LibreOffice** and **WPS Office** are among the most popular and versatile options. These office suites exhibit a range of distinctive strengths—ranging from sleek interfaces to seamless compatibility with Microsoft Office, as well as robust open-source communities and collaborative features.  

Whether these tools are intended for personal use, business contexts, or cooperative projects, they guarantee that users have access to reliable resources that cater to a wide array of productivity needs. However, the benefits they offer can sometimes be overshadowed by the ease of conventional software. Although many people may be hesitant to accept such a change, it's crucial to acknowledge the potential advantages of embracing these options (because they frequently provide remarkable functionality without any expense). This transition can result in enhanced productivity and cooperation across different settings.

Let's now explore the installations of the free and open-source office suites mentioned.

### WPS Office

[WPS](https://www.wps.com/) Office is an extremely compatible, feature-rich, and lightweight office suite. It has the ability to manage text in spreadsheets, presentations, writers, and PDF files. It acts as a practical and knowledgeable advisor to assist you in increasing the effectiveness of your work. In addition to being a perfect substitute for LibreOffice, WPS allows Linux users to avoid depending on external Windows computers for document processing.

*Key Features:*

- **Cross-Platform Compatibility**: Smoothly runs on Windows, macOS, Linux, Android, and iOS.

- **Compatibility with Microsoft Office**: Reads and writes.docx,.xlsx, and.pptx files with ease.

- **Lightweight and Fast**: Uses fewer system resources compared to LibreOffice or Microsoft Office.

- **Built-in PDF Tools**: Allows editing, conversion, and merging of PDFs.

- **Tab-Based Interface**: Keeps documents organized in tabs, much like web browsers.

- **Free to Use**: Core features are free, with the option to upgrade to a premium version for more advanced features.

- **Cloud Support**: Integrates with WPS Cloud to sync files easily across devices.

- **User-Friendly Interface**: New and intuitive UI helps in a relatively smooth transition from Microsoft Office.

#### Install WPS Office On Ubuntu

The following detailed instructions will help you download and install WPS Office on Ubuntu. We shall look at three methods that one can choose to install WPS Office on Ubuntu.

##### Method 1: Install WPS Officе Using GUI

With the GUI, installing WPS Office is simple. First search Ubuntu Software in the application menu. Once you launch the Ubuntu software store,search for "**WPS**." In the results, click "**WPS Office**’’ like as shown:

![](/home/chiloba/Pictures/productivity%20Folder/Productivity-In-Everyday-Use-37.png)

In the next step, click the **instal**l button, and you’ll be prompted to enter a password to confirm the installation. By doing so, WPS will be installed!

##### Method 2: Install WPS Office Using dpkg

Head over to the [WPS](http://www.wps.com/) Office Linux downloads page and click on the Deb package button to download the Debian binary installer.

- Verify that the deb package has downloaded by going to `Downloads`.

- Next, "right-click" on the WPS Office download package and select the option to "`Open With Other Application`."

- Once you click Open with other application, select Software Install and hit the `install` button.

- Then, verify WPS Office's **terms and conditions** and wait for WPS to finish installation in a few minutes.

*Alternatively*, one can use the terminal to install the downloaded file. But by default, everything  downloaded using a browser ends up in the system's Downloads folder. 

Thus, start by switching to the download directory using the **cd** command by running:

```bash
cd ~/Downloads
```

The downloaded binaries can now be installed using the **APT** package management command tool.

```bash
sudo apt install ./wps-office_*_amd64.deb
```

When the installer asks to install Microsoft fonts during the package configuration, read the terms and conditions and click "**Ok**" and  agree to the terms of the EULA license by clicking yes and wait for installation to end. 

Are Apt `install./` Useful? 

- **Dependency management**: Installs any necessary packages automatically.  

- **Not as complicated** as `dpkg -i`: Dependencies can be fixed without a separate command.

##### Method 3: Using Snap (Recommended for Updates)

First install snap if you've not yet done so. To install it, do the commands listed below.

```bash
sudo apt update
sudo apt install snapd
```

Then execute the below line to install WPS Office.

```bash
sudo snap install wps-office
```

It takes a few minutes to complete the installation based on the internet speed.

##### Launching WPS Office

In the application menu, search for WPS, and it will display various components. You can choose either Writer, Excel, or PowerPoint and open it. For instance, PowerPoint.

![](/home/chiloba/Pictures/productivity%20Folder/Productivity-In-Everyday-Use-36.png)

WPS Office may improve your everyday workflow and productivity with its feature-rich programs, interface, and compatibility with Microsoft Office file types.

You may experience a seamless and effective office suite on your Ubuntu system, allowing you to do your chores with ease and professionalism.

### FreeOffice

FreeOffice is an absolutely free, open-source alternative tool to MS Office introduced by the German house SoftMaker Software GmbH. It offers compatibility with all ranges of MS suite formats. It is considered one of the best options against Microsoft Office. Although Free Office does not offer all the applications included in Microsoft Office, it has mainly covered most commonly used day-to-day applications and focuses on text created as an alternative option to MS Word and a presentation similar to PowerPoint.

*Here is why FreeOffice stands out:*

- **User-Friendly**: The intuitive interface it offers makes switching from other office suites easy.

- **Feature-rich**: Equipped with a complete suite of word processing, spreadsheet, and presentation tools.

- **Compatibility**: Open and save documents in Microsoft Office formats with full compatibility.

- **Free and Reliable**: Free of cost, though at no cost over performance or functionality.

The following packages make up FreeOffice:

- TextMaker is a word processor.

- SoftMaker Presentations is a tool for creating graphics and presentations.

- BasicMaker is a programming tool that works similarly to VBA.

- PlanMaker is a spreadsheet program.

#### Install FreeOffice on Ubuntu

Let’s dive into installations of FreeOffice using two options, such as:

- Using the Softmaker repository.

- Using a .deb file

##### Option 1: Using the SoftMaker repository.

Any version of FreeOffice can be downloaded and installed on Ubuntu via a repository. Start by adding the repository's GPG key using the commands:

If wget is not installed on the system, do so with the below command since wget is used to download files from the internet.

```bash
sudo apt update && sudo apt install wget
```

Once installed, run the commands below to add the GPG key. 

```bash
sudo -i
mkdir -p /etc/apt/keyrings
wget -qO- https://shop.softmaker.com/repo/linux-repo-public.key | gpg --dearmor > /etc/apt/keyrings/softmaker.gpg
```

Explanations of the commands:

- `sudo -i` – switch to root user.

- `mkdir -p /etc/apt/keyrings` – Build a directory to hold the keys.

- `wget -qO- <url>` – To download the GPG key.

- `| gpg --dearmor > /etc/apt/keyrings/softmaker.gpg `– Save the key for APT after converting it to binary format.

Next, add Ubuntu's SoftMaker repository by running:

```bash
echo "deb [signed-by=/etc/apt/keyrings/softmaker.gpg] https://shop.softmaker.com/repo/apt stable non-free" | sudo tee /etc/apt/sources.list.d/softmaker.list > /dev/null
```

*Explanation of the command*:

- **`tee`**: This command enables the use of redirection `(>)` and writes the output to the file with elevated permissions respectively.Indicate a unique home directory.

- **`> /dev/null`**: This will prevent duplicate output to the terminal by suppressing the standard output.

This command will add the SoftMaker repository to your system's APT sources, enabling installation and updating of the software via the package manager.

Then refresh your APT package index with the following command.

```bash
sudo apt update
```

With the repository now successfully added in the system, we can install the latest FreeOffice 2024 in Ubuntu with the command:

```bash
sudo apt install softmaker-freeoffice-2024
```

Wait for the installations to complete.

##### Option 2: Install FreeOffice on Ubuntu using deb file

This might be of interest because it is a simple approach for anyone who doesn't want to deal with the headache of adding the repository to Ubuntu in order to install FreeOffice.

Simply [visit the official download page of FreeOffice](https://www.freeoffice.com/en/service/tips-and-tricks/linux) and download the FreeOffice .deb file:

Launch the terminal and use the **cd** command to navigate to the directory containing the **.deb** file once the download is complete.

It will be found in the Downloads directory for the majority of users:

```bash
cd ~/Downloads
```

To install the .deb file downloaded above in Ubuntu, use the command below:

```bash
sudo apt install ./softmaker-freeoffice*.deb
```

With this command, the SoftMaker FreeOffice package (.deb file) is installed using APT from the current directory.

If you install FreeOffice this way, you will need to set up automatic updates on Ubuntu. Run:

```bash
sudo /usr/share/freeoffice2024/add_apt_repo.sh
```

We need to update the APT package index now that we've added a new APT source. As a result, the system can identify the recently added source and register the FreeOffice packages that are ready for installation. Execute the below command.

```bash
sudo apt update
```

 That’s all about FreeOffice installations on Ubuntu.

##### Launch FreeOffice on Ubuntu

You can launch any FreeOffice suite component by navigating to the 'Office' category in your system's program menu using the following path:

**Activities > Show Applications > FreeOffice {Text Maker, Presentations, PlanMaker}**

After launching FreeOffice, for instance, you select PlanMaker; you can as well create spreadsheets like you used to in MS Excel. FreeOffice provides you with two alternatives for saving your Plan Maker document, which are listed below.. Choose one option and hit the **OK** button.

![](/home/chiloba/Pictures/productivity%20Folder/Productivity-In-Everyday-use-21.png)

For your productivity needs, FreeOffice is a dependable and easy-to-use office suite that works well with Ubuntu and is available for free. We advise experimenting with it, personalizing it to your liking, and learning about its capabilities for creating presentations, managing spreadsheets, and drafting documents.

### **Apache OpenOffice**

OpenOffice is an open-source software suite that provides many productivity tools. It's a very good alternative to proprietary office suites, such as Microsoft Office, and is widely used by companies and individuals across the globe. OpenOffice includes several word processing, spreadsheet, presentation, graphic, and database tools. One of the key features of OpenOffice is its free nature; hence, anyone can download and use it without any licensing fee.

**The components of Apache OpenOffice:**

- [Writer](https://www.openoffice.org/product/writer.html) a word processor that can be used for anything from a letter to write up to the production of an entire book.  

- [Calc](https://www.openoffice.org/product/calc.html) is a comprehensive spreadsheet that includes all of the tools you'll need to calculate, analyze, and show your data in numerical reports or eye-catching graphs.

- [Impress](https://www.openoffice.org/product/impress.html) fast and powerful, the most intelligent way to create powerful multimedia presentations.

- [Draw](https://www.openoffice.org/product/draw.html) allows you to create everything from simple schemes to dynamic 3D illustrations.

- [Base](https://www.openoffice.org/product/base.html) Apache OpenOffice allows for database manipulation, including table creation, form editing, query creation, and report generation.                  

- [Math](https://www.openoffice.org/product/math.html) enables the creation of equations by using a graphical user interface or directly typing the formula into the equation editor.

#### Install OpenOffice on Ubuntu

The steps listed below will help you install OpenOffice on Ubuntu:

**Remove LibreOffice**

To guarantee a seamless installation, you can take the following actions if LibreOffice is already installed on your Ubuntu system and you wish to uninstall it before installing OpenOffice.

Open the terminal using Ctrl+Alt+T and run the below command to remove LibreOffice and its packages.

```bash
sudo apt remove libreoffice*
```

Input password when prompted. After the removal procedure is finished, you can use the following command to remove any remaining files and dependencies:

```bash
sudo apt autoremove
```

Any unnecessary packages and dependencies that are installed with LibreOffice will be deleted by this command.

**OpenOffice not available in the Ubuntu Software Center because?**

- The development of OpenOffice has halted, and the most popular open-source office suite is LibreOffice.  

- OpenOffice is not accessible through official repositories or delivered as a Snap.

**Recommendation for Most Users**:

- LibreOffice is a more up-to-date substitute that may be downloaded as a Snap or straight from the Ubuntu Software Center.  

- *The most dependable and straightforward installation technique is the **.deb** file if you particularly want "Apache OpenOffice."*

Apache OpenOffice can be installed using the following  method:

- From CLI (command line)

##### Install Apache OpenOffice From CLI

Using the terminal to install OpenOffice on Ubuntu is one of the most popular methods. Unluckily, you will need to download and install OpenOffice manually because it is not accessible in the "normal Ubuntu repository." To install OpenOffice from the official website using the terminal, follow these steps:

Download the latest version of Apache OpenOffice from the [Apache OpenOffice homepage](https://www.openoffice.org/download/index.html). Select either the 64-bit or 32-bit Debian version from the download page.

The file can be downloaded via a "web page" or by using the <u>**wget**</u> command-line tool, which is used for downloading files from the web. To use wget command, it must first be installed on the system if not yet installed.

```bash
sudo apt update && sudo apt install wget
```

Begin to download the OpenOffice installation package by executing:

```bash
VER=4.1.15
wget "https://downloads.sourceforge.net/project/openofficeorg.mirror/${VER}/binaries/en-US/Apache_OpenOffice_${VER}_Linux_x86-64_install-deb_en-US.tar.gz"
```

**The advantages of using a variable**:

- *Upgrade to a new version* is easy and only requires changing the version number (VER).

- *Reusable Commands*: Several versions can be installed by the same script without requiring human modifications.

Navigate to the download directory using the **cd** command and **extract** the downloaded OpenOffice archive file with the next command:

```bash
cd ~/Downloads
tar xvf Apache_OpenOffice_${VER}_Linux_x86-64_install-deb_en-US.tar.gz
```

- **tar**- (tape archive) is a file archiving software.  

- **x** - This option is use to extract the contents of the archive.  

- **v** - Means verbose mode it displays the extraction process by file.  

- **f** - Use the provided file (in this case, an archive file).  
  
  After files have been extracted, the main directory is "**en-US/DEBS/**". Go to the "en-US/DEBS/" directory, which contains the OpenOffice Debian package installation.

```bash
cd en-US/DEBS
```

Once in the en-US/DEBS/ directory, install the Debian packages of OpenOffice and its utilities with the given command:

```bash
sudo apt install ./*.deb
```

Now, you have to install the Debian packages available in the desktop-integration directory for the integration of desktop apps of the utilities.

First, move to the **desktop-integration** directory by running the below command.

```bash
cd desktop-integration/
```

Then install the Debian packages that are necessary for desktop integration.

```bash
sudo apt install ./openoffice4.1-debian-menus_*.deb
```

##### Launch and Use OpenOffice On Ubuntu

Hold off until the installation is complete. Go to the `Applications` menu and type `Office` in the search bar and click OpenOffice icon. 

Once you launch OpenOffice, you'll get a **welcome wizard** page. Click the **Next** button to proceed.

- In the next page, set your **username** and click the **Finish** button. 

- Select the **database**,either new or use existing and click the **Finish**.

- In the Save and Proceed step, choose how to proceed after saving the database; hence click **Finish**.

Following that, the Apache OpenOffice will launch using the interface that is displayed below.

![](/home/chiloba/Pictures/productivity%20Folder/Productivity-In-Everyday-Use-23.png)

Select the desired program from the main menu (Writer, Calc, Impress, Draw, or Base). *Often save your work using the "Save" button or the "Ctrl+S" shortcut. Export your database, spreadsheet, presentation, graphic, or document to a file type that other people may access.*

OpenOffice is a robust productivity suite with tools in the areas of word processing, spreadsheets, presentations, graphics, and databases—making it one great choice for an alternative to the proprietary office suites of Microsoft Office. It has proven to be a really handy tool for businesses and organizations across the world, besides individual users.

### LibreOffice

LibreOffice is free and open-source office suite software, widely regarded as a strong alternative to proprietary office suites such as Microsoft Office. LibreOffice is a great option for Ubuntu users seeking a complete office solution without the license fees associated with commercial programs because of its open-source nature and extensive feature set. 

*Key Features of LibreOffice:*

- The **versatile suite** consists of Word Processing (Writer), Spreadsheets (Calc), Presentations (Impress), Vector Graphics (Draw), Databases (Base), and Formula Editing (Math).

- **Broad File Format Compatibility**: Outstanding compatibility with a large number of file formats, including native support for OpenDocument Format (ODF) and Microsoft Office document files.

- **Interface Personalization**: A versatile user interface featuring a range of toolbars, themes, and icon styles is available for customization.
  Wide Language Support: It is suited for a worldwide user base because it is available in more than 40 languages.

- **Advanced Scripting Capabilities:** Enables sophisticated automation and customization by supporting a variety of scripting languages, including Python.

- **Support for Integrated Cloud**: Able to connect with multiple cloud services for online document editing and teamwork.

- **Strong Formatting and Styles**: Provides advanced formatting and style choices for expert document design and layout.

- **Advanced Spreadsheet Features**: Calc offers a large selection of sophisticated features and tools for analyzing and visualizing data.

Let's examine how to install it in the next section.

#### Install LibreOffice on Ubuntu

LibreOffice installation on Ubuntu is simple and can be accomplished in a number of ways, including:

- Ubuntu Software Center (GUI Method).

- Terminal (Command Line Method).

- PPA Method.

- Snap (Canonical's Official Method).

##### Option 1: Using Ubuntu Software Center (GUI Method)

(*The simplest and best option for novices*)

Install LibreOffice via the Graphical User Interface (GUI) by following the instructions below.

- Locate **Ubuntu Software** by clicking on "Show Applications" (grid symbol at bottom-left).   

- Use the search bar to look up **LibreOffice**, then click on it from the list of results:

- Click the **Install** button and input your password. If prompted in order to begin installation.
  
  ![](/home/chiloba/Pictures/productivity%20Folder/Productivity-in-Everyday-use-26.png)
  
  The entire LibreOffice suite—Writer, Calc, Impress, etc.—will be installed as a result.

##### **Option 2: Using Terminal**

Press Ctrl + Alt + T or search for "Terminal." (*For quicker installation and package control*)

LibreOffice may now be installed with the **apt** package manager. Execute the below command.

```bash
sudo apt install libreoffice
```

After installation is complete, check the installation.

```bash
libreoffice --version
```

Installed version should be the output of the above command.

##### Option 3: Using the PPA Method

As Ubuntu formally offers PPAs (Personal Package Archives) via Launchpad, including the LibreOffice PPA repository, PPAs are the most popular and advised method of installing any third-party application on Ubuntu.  

It's easier to obtain the most recent stable version and maintain upstream compatibility by using the official LibreOffice PPA. To install LibreOffice via the terminal from the PPA repository, let's take the actions listed below:

```bash
sudo add-apt-repository ppa:libreoffice
sudo apt update
sudo apt install libreoffice -y
```

After the installation is finished, go to <u>Activities</u> and look up "<u>LibreOffice</u>." All of the LibreOffice applications will be visible to you.

##### Option 4: Using Snap

Snap packages in the Snap store provide access to the latest versions of LibreOffice. To install it, do the commands listed below.

```bash
sudo apt install snapd
sudo snap search libreoffice
sudo snap install libreoffice
```

Await the completion of the installation.

##### **How to launch LibreOffice on Ubuntu**

LibreOffice may be opened with the Ubuntu desktop environment in the "**Activities**" section; search **LibreOffice** and select it from the list of results.

If you decide to use terminal launch it, run:

```bash
libreoffice
```

### **OnlyOffice**

[OnlyOffice](http://onlyoffice.com/) is an open-source, collaborative office suite. It has three editors for text documents, spreadsheets, and presentations that are fully compatible with Office Open XML formats and allow for collaborative editing in real time. Besides that, OnlyOffice is an entire collaboration platform providing CRM, projects, document management system, mail, calendar, blogs, forums, chat, and also third-party online services such as Nextcloud, ownCloud, Alfresco, Confluence, SharePoint, Liferay, HumHub, or your own online application.

*Key Features OnlyOffice:*

- Support for online editing of text documents, spreadsheets, and presentations.

- Real-time collaborative editing (two co-editing modes, change tracking, version history and comparison, comments and mentions, built-in chat).  

- Different access levels (full access, review, form filling, commenting, read-only, and custom filter for spreadsheets).  

- All common formats are supported, including DOC, .DOCX, .TXT, .ODT, .RTF, .ODP, .EPUB, .ODS, .XLS, .XLSX, .CSV, .PPTX, and HTML.  

- Built-in plugins and micros provide additional editing possibilities.  

- The ability to create and connect third-party plugins via API.

If you want to try OnlyOffice, check the below instructions in the below section. 

#### Install OnlyOffice Desktop Editors (Free, Personal Edition)

By following the steps given in this section you'll be able to set up OnlyOffice on Ubuntu System. Well will cover the following options on how to install OnlyOffice.

- Using .deb package
- From snap package 

##### Option 1: Install OnlyOffice Using Snap (Easy Method)

Snap packages are self-contained, include all dependencies, and are therefore quite easy to install, with fewer chances of dependency problems.

To install ONLYOFFICE on Ubuntu via Snap is the simplest method. First, ensure that you've installed Snap. If not, run the below commands:

```bash
sudo apt update && sudo apt install snapd
```

Once you installed Snap, you can now install OnlyOffice in the Snap store.

```bash
sudo snap install onlyoffice-desktopeditors
```

After completing the installation, you can search OnlyOffice  in the Activities menu and launch it.

##### Option 2: Install OnlyOffice with DEB Package

Get the Deb file first by visiting the official [OnlyOffice](https://www.onlyoffice.com/download-desktop.aspx) page.

Alternatively, you can utilize the wget command in the terminal and install it directly. If wget is not yet installed in the system, install by running:

```bash
sudo apt update && sudo apt install wget
```

You can now download the OnlyOffice with the command below.

```bash
 wget https://download.onlyoffice.com/install/desktop/editors/linux/onlyoffice-desktopeditors_amd64.deb
```

Navigate to the download directory using **cd** command where it stores the downloaded file.

```bash
cd ~/Downloads
```

Then run the below command to install the deb package.

```bash
sudo apt install ./onlyoffice-desktopeditors_amd64.deb
```

##### How to Lauch ONLYOFFICE On Ubuntu

Upon finishing the installation, on your desktop environment you can launch OnlyOffice by searching `OnlyOffice` from the **Activities** menu and click it's icon.

You can as well launch through command line by executing:

```bash
onlyoffice-desktopeditors
```

After a successfull installation, OnlyOffice will be opened.

![](/home/chiloba/Pictures/productivity%20Folder/Productivity-In-Everyday-Use-25.png)

At this point, you can select the program you wish to utilize. Additionally, you can connect to the cloud if you already have an account, or you can just create one to integrate.

ONLYOFFICE Desktop Editors is an elegant and professional office suite that is well in line with paid alternatives. Whether advanced editing or basic office capabilities are needed, ONLYOFFICE is a full-featured, reliable, and future-proof answer for increasing productivity. Numerous integration options are available, including ownCloud, Nextcloud, Liferay, HumHub, Nuxeo, and others.

## **Collaboration Tools**

Collaboration tools are an integral part of any organization in improving productivity, communication, and teamwork. Using these platforms, teams can easily collaborate on tasks, whether in-office or remotely, through their instant messaging, video conferencing, file-sharing features, and more.  

With progressive adoption of hybrid and remote work arrangements, organizations have felt the need for collaboration tools in order to drive effective communication, optimize workflows, and generally enhance productivity within teams. All the way from informal team discussions to high-level organizational meetings, it serves to connect teams and departments, facilitating the continuum of projects without interruptions.

In this module, we will cover some of the most commonly used collaboration tools; that is,

- **Microsoft Teams**
- **Slack**
- **Rocket.Chat Client**
- **Zoom**
- **Mattermost**
- **Telegram Desktop**
- **Cisco Webex**
- **Jitsi Meet**

Installing Microsoft Teams will be our first step, and then the others in order.

### Microsoft Teams

Microsoft Teams is the best messaging app for your company; it's a platform for meetings, file and app sharing, real-time collaboration, and even the occasional emoji! Everything is in one location, open to the public, and within reach of everyone.

*Features of Microsoft Teams*:

- **Collaboration and File Sharing**: Easy integration with Office 365, SharePoint, and OneDrive ensures that users collaborate in real time on documents with ease.

- **Tabs and Connectors**: Customizable tabs within channels provide single-click access to frequently used services and applications.

- **Chat**: Persistent group and individual conversations with threaded discussions.

- **Meetings**: Host webinars with larger audiences and virtual meetings for up to 1,000 people.

- **End-to-End Encryption**: Securely communicate and protect data within conversations with end-to-end encryption.

- **Integrations and Apps**: Integration with Microsoft applications such as Planner and Power BI, third-party applications like Trello, Asana, and GitHub. 

- **Task management**: Assign and track tasks using integration with Microsoft Planner and To Do.

- **Screen Sharing**: Share your screen in meetings for better collaboration.

- **Offline Mode**: You can view files and conversations even when you're offline.

#### Install Microsoft Teams on Ubuntu System

We will install Microsoft Teams using Snap on Ubuntu. Canonical made Snap, a system for installing and packaging software for technology that uses the Linux kernel and the systemd init system.  

If you do not have Snap installed in your Ubuntu system, install it as follows: 

```bash
sudo apt update && sudo apt install snapd
```

Run the following command to install Microsoft Team;  

```bash
sudo snap install teams-for-linux
```

##### Launch Microsoft Teams on Ubuntu

Once Microsoft Teams has been successfully installed on Ubuntu, launch it by selecting Teams from the menu and searching for ”Teams for Linux” or by typing “teams-for-linux” in the command line interface, as indicated below.

i) From the command line interface

```bash
teams-for-linux
```

ii) From the Desktop Environment

Go to Menu and search for “**Teams for Linux**” to launch.

iii) To use Microsoft Teams, `register for an account or log in `by providing your company’s email if you already have one and click “**Next.**”

![](/home/chiloba/Pictures/productivity%20Folder/Productivity-In-Everyday-Use-24.png)

Enjoy collaborating on projects and daily work communications with coworkers, outside consultants, vendors, etc., using the Microsoft Teams program on Ubuntu Linux.

### Slack

The most widely used collaboration tool in the business sector is Slack. Since acquiring HipChat, the company has taken the lead in the collaboration space, enabling your team to collaborate and complete tasks. Slack revolutionizes the way businesses achieve their objectives by integrating people, processes, data, agents, and AI into a single conversational interface.  

*Features of Slack:*

The following are some great features of Slack.  

- **File Sharing:** Slack users can share directly with others their documents, photos, and other data.

- **Channels**: Discussions occur within channels, and these could be team-based, project-based, or based on topics. Channels are available either as private—that is, available only to selected users—or public, where it's for everyone in the workplace.

- **Direct Messaging (DM)**: Enables group and individual conversations outside of channels.

- **Notifications**: Easily customize notifications to get what users need to know without the noise.

- **Search Functionality**: Powerful search functionalities are enabled by Slack that enable users to locate files, conversations, and messages fast.

- **Integration of Tools**: Slack integrates with tons of third-party apps like Jira, Trello, GitHub, Google Drive, and many others that make processes better.

- **Slack Connect**: Common channels for collaborating with outside companies.

### Install Slack on Ubuntu System

We'll go over how to install Slack on an Ubuntu system using the following methods.

##### Method 1: Using .deb file

We will use the wget utility to obtain the Slack `.deb` file. If you do not have wget on your Ubuntu, run the following command to install it.

```bash
  sudo install wget
```

Obtain Slack .deb file  

```bash
VERSION=”4.41.105”
wget wget https://downloads.slack-edge.com/desktop-releases/linux/x64/$VERSION/slack-desktop-$VERSION-amd64.deb 
```

Install Slack using dpkg tool.

```bash
sudo apt install ./slack-desktop-$VERSION-amd64.deb
```

##### Method 2: Using Snap

Snap, developed by Canonical, is a system for packaging and installing software for devices that use the systemd init system and the Linux kernel.

Install Snap using these steps if it isn't already installed on your Ubuntu system:

```bash
sudo apt update && sudo apt install snapd
```

Run the following command to install Slack;  

```bash
sudo snap install slack
```

##### Launch Slack on Ubuntu

After Slack has been successfully installed on Ubuntu, open it by typing "`slack`" into the command line interface or choosing Slack from the menu, as shown below.

i) From the command line interface.

```bash
slack
```

ii) From the Desktop Environment.

Go to Menu and search for “`slack`” to launch.

iii) Sign in to start using Slack on Ubuntu.
![](/home/chiloba/Pictures/productivity%20Folder/Productivity-In-Everyday-Use-22.png)  

Organizations love Slack because of its easy-to-use UI and many tool integrations, which make it a vital tool for today's dispersed teams.

## Rocket.Chat Client

Rocket. Chat Client is a cross-platform (desktops and mobile) application that establishes a user's connection to Rocket.Chat servers to facilitate communication and collaboration. It plays a key role within the Rocket.Chat ecosystem, offering a vehicle for team chat, video calls, and file exchange, and facilitating both internal and external collaboration.

*Key Features of Rocket.Chat Client:*

- **Real-time messaging collaboration**: Participate in one-on-one, team, and group conversations.

- **Video and Audio Conferencing**: Start or join video/audio conversations natively within the client.

- **File Sharing and Integration**: Share documents, pictures, and files easily in chat. Integrates with tools like Google Drive, Dropbox, and GitLab.

- **Open source Self-hosted**: On-premise Rocket.Chat servers for increased data privacy.

- **End-to-End Encryption**: Encrypted communication and compliance-compliant infrastructure.

#### Install Rocket.Chat Client on Ubuntu

Here are the steps to be covered in order to install Rocket.Chat Client on Ubuntu. We shall look at two alternative methods one can use for installation.

##### Method 1: Install Rocket.Chat via Snap (Recommended)

This approach assures automatic updates and ease of maintenance. To install Rocket.Chat Client, run the below commands:

```bash
sudo apt update
sudo apt install snapd
sudo snap install rocketchat-desktop
```

Upon completion of the installation, Rocket.Chat can be found in the applications menu.

##### **Method 2: Install via .deb Package (Manual Installation)**

Now let's walk through how to install the Rocket.Chat desktop application on Ubuntu via the **.deb** package.

Ensure that your system is up-to-date and install the `wget` command we shall use to download files.

```bash
sudo apt update && sudo apt install wget
```

See the official [Rocket.Chat GitHub Releases page](https://github.com/RocketChat/Rocket.Chat.Electron/releases) for the latest version. Alternatively, do it via command line by downloading the **.deb** file straight from it. 

We will query the most recent version of git using the `curl` command. Check if curl is installed by using the command below; if not, it will be installed.

```bash
sudo apt install curl
```

Fetch the latest version from GitHub API by running:

```bash
curl -s https://api.github.com/repos/RocketChat/Rocket.Chat.Electron/releases/latest | grep tag_name | cut -d '"' -f 4 | sed 's/v//'

4.1.2
```

-  Curl operates in "silent" mode when the `-s` option is used, which prevents it from displaying progress or error messages. 

After fetching the latest version, execute the below command to store variable `VERSION`.

```bash
VERSION=$(curl -s https://api.github.com/repos/RocketChat/Rocket.Chat.Electron/releases/latest | grep tag_name | cut -d '"' -f 4 | sed 's/v//')
```

Then download the `.deb` package. 

```bash
wget https://github.com/RocketChat/Rocket.Chat.Electron/releases/download/$VERSION/rocketchat-$VERSION-linux-amd64.deb
```

After the download has finished, install the package with the following APT command.

```bash
sudo apt install ./rocketchat-$VERSION-linux-amd64.deb
```

##### **Launch Rocket.Chat**

Press Super (Windows key) and type **Rocket.Chat** and click its icon to launch it on the desktop environment.

Alternatively, you can use the terminal to launch it by entering:

```bash
rocketchat-desktop
```

 Once you launched it, enter your `server URL `and click `connect`.

![](/home/chiloba/Pictures/productivity%20Folder/Productivity-In-Everyday-Use-27.png)

Rocket. Chat has allowed organizations to develop their own communication ecosystem, which is less dependent on external services but which still gives them the ability to remain in control of their data. Because of its flexibility and its powerful feature set, it is one of the most robust candidates for any group that desires to increase efficiency and productivity and increase intersubjectivity.

### Zoom

Zoom is one of the leading video conferencing software applications, and these video conferencing applications have great popularity for virtual meetings, webinars, and group work. Due to its ease of use, robustness, and versatility, it is an appropriate solution for telework, distance learning, and big groups.

*Features of Zoom:*

- **Ease of Use**: Very intuitive and simple UI.  

- **High-quality video/audio:** Clear communications even over very low bandwidths.

- **Screen Sharing**: Share either your whole screen or just one window.  

- **Meeting Recording:** Record meetings for later review.  

- **Virtual Backgrounds**: Personalize your conference room.  

- **Security** involves end-to-end encryption and password-protected meetings.

#### Install Zoom on Ubuntu

Now that you've understood what Zoom is, let's now see how to install it on an Ubuntu system. We shall demonstrate using different methods such as:

- Install Zoom via .deb

- Install Zoom via Snap

##### Method 1: Install Zoom via .deb

To install the Zoom client on Ubuntu, use the `.deb` package approach, which involves downloading the official Zoom package from the Zoom website. Zoom is not available in the Ubuntu repository by default.

To download this deb package, open your terminal using Ctrl+Alt+T and run the command below to download the  latest version. Use the `wget` command to download it.

If the wget command is not yet installed, install it by running:

```bash
sudo apt install wget
```

Now download the package.

```bash
wget https://zoom.us/client/latest/zoom_amd64.deb
```

By doing this, the most recent Zoom package version will be downloaded to your system.

After the download is finished, use the following command to install the package:

```bash
sudo apt install ./zoom_amd64.deb
```

Wait for a few minutes to end the installations, and you'll be able to use video conferencing and collaboration in your system.

##### Method 2: Install Zoom via Snap

Alternatively, you can use Snapcraft, a package manager that is pre-installed on the majority of Ubuntu desktops, to install Zoom on Ubuntu. In most cases, this approach is quicker and easier than installing Zoom via a .deb package.

Use the given command to confirm that Snapcraft is installed on your computer before beginning:

```bash
sudo apt install snapd
```

It's simple to install Zoom with Snapcraft; simply execute the following command to set up Zoom on your system:

```bash
sudo snap install zoom-client
```

##### Launch and Use Zoom On Ubuntu

After installation, you can launch Zoom using the desktop environment by selecting **Activities** and typing "**Zoom**" into the search bar and clicking it. Or you can use the command line by running:

```bash
zoom
```

You'll see the below window.

![](/home/chiloba/Pictures/productivity%20Folder/Productivity-In-Everyday-Use-28.png)

You can now  "join a meeting"  and **enter your meeting ID** or "Sign" in if you have an account.

Zoom is a necessity in today's work environment, offering effortless communications and collocated work across groups, without location. Its multifunctionality, for instance, video conferencing sessions, webinars, screen sharing, and real-time collaboration, makes it an essential basis for remote and hybrid work productivity.

### Mattermost

Mattermost is a secure, open-source messaging and collaboration tool for teams and organizations. It is often seen as a viable alternative to the tools, such as Slack, with the advantage of 100% control over data and privacy. Mattermost is installable and available on the cloud as well, so it is a good option for enterprises that are prioritizing security and customization.

 *Features of Mattermost:*

- **Team Collaboration**: Real-time messaging, file sharing, and seamless collaboration for teams.

- **Integrations**: Integrates with GitLab, Jira, and lots of other CI/CD pipelines.  

- **Highly Secure**: Self-hosted options, industry standard compliance, and end-to-end encryption make it secure.  

- **Customizable**: It's open-source and highly extensible to organizational needs.

- **Scalable:** Scales from small teams to large enterprise usage.

- **Offline Access:** Provides offline access to previously synchronized files and communications.

#### Install Mattermost On Ubuntu

We shall demonstrate the installation of Mattermost on Ubuntu using various methods. Every technique is appropriate for a variety of user preferences, including those who want simplicity .deb package, Snap's` stability.

##### **Method 1: Install Mattermost via Official .deb Package**

Go to the official Mattermost [releases]([Releases · mattermost/desktop · GitHub](https://github.com/mattermost/desktop/releases))  page or download the .**deb** package with wget. Begin by installing wget if you've not done it before.

```bash
sudo apt update && sudo apt install wget
```

Run the below commands to download Mattermost. Substitute the most recent release version with version **5.10.2** below.

```bash
 VERSION="5.10.2"
 wget https://releases.mattermost.com/desktop/$VERSION/mattermost-desktop_${VERSION}-1_arm64.deb 
```

The previously downloaded package can be installed using the "apt" command:

```bash
 sudo apt install ./mattermost-desktop_${VERSION}-1_amd64.deb
```

Upon finishing the installation, Mattermost will be accessible in the applications menu.

##### **Method 2: Install Mattermost via Snap**

Installing Mattermost using Snap is the easiest method. First, install Snap if not yet installed.

```bash
sudo apt update && sudo apt install snapd
```

Install Mattermost using the Snap package manager:

```bash
sudo snap install mattermost-desktop
```

##### Launch Mattermost on Ubuntu

Once done with the installation, you can launch Mattermost using the command line or desktop environment **application** menu and type **Mattermost** in the search field.

I) To launch using the command line. Run:

```bash
mattermost-desktop
```

ii) Using desktop Environment:

Go to the application menu and search **Mattermost.** After launching, click `Get started` and enter server details and hit the Connect button.

![](/home/chiloba/Pictures/productivity%20Folder/Productivity-In-Everyday-Use-29.png)

In other words, Mattermost improves productivity by offering an all-in-one, secure, and integrated communication solution for teams. The platform is so focused on real-time collaboration, smooth workflows, and customizations that have made it so strong to amply drive efficiency at full throttle, enabling teams to keep their eye on the ball. getting the job done.  

### **Telegram Desktop**

Telegram is a cloud-based messaging service oriented towards privacy, security, and speed. With the use of an internet connection, it allows its users to communicate in various ways, send messages, and send media. Telegram is available on web browsers, desktop PCs, and mobile devices.

*Features of Telegram:*

Some of the key features of Telegram are as follows. 

- **Messaging**: The users can send documents, movies, voice messages, text messages, etc.

- **Voice and Video Calls**: Telegram users can speak in real time to their friends or colleagues; both voice and video calls are supported.

- **File Sharing**: It helps users share big documents or media since it supports a file as big as 2 GB.

- **Channels**: Telegram allows the creation of private or public channels, which allow large audiences to hear from a single admin or groups of administrators.

- **End-to-End Encryption**: Telegram does provide end-to-end encryption in its "Secret Chats" mode, ensuring that only the sender and receiver can read the messages. While standard cloud conversations are encrypted, they are not by default end-to-end encrypted.

- **Bots**: Telegram supports bots, automated programs that can manage activities ranging from processing payments and organizing tasks to sending news updates.

- **Customizable**: From the settings of a single chat to setting up themes and notification preferences, Telegram is customizable to a wide degree.

- **Security and Privacy**: Telegram's respect for users' privacy is well acknowledged. It features anonymous forwarding and self-destructing messages and doesn't share data with outside parties.

- **Groups**: It supports the creation of groups with up to 200,000 users for extensive

communication and collaboration.

#### Install Telegram Desktop on Ubuntu System

Here are the steps we'll take to install Telegram Desktop on an Ubuntu system.

##### Step 1: Download Telegram .tar.xz Package

We will use the wget utility to obtain the Telegram.tar.xz package for Linux. If you do not have wget on your Ubuntu, run the following command to verify and install it. 

```bash
sudo install wget
```

i) Obtain the Telegram .tar.xz package for Linux. Use the most recent version instead.

```bash
VERSION=”5.9.0”
wget https://td.telegram.org/tlinux/tsetup.$VERSION.tar.xz
```

ii) To extract the aforementioned file, use the tar command.

```bash
tar -xJf tsetup.$VERSION.tar.xz
```

Breakdown of the above command:

- `tar`: It is a command-line utility for working with **.tar** archives. It is capable of creating, extracting, and managing <u>.tar archives.</u>

- `-x`: With this option,<u> tar</u> is instructed to extract files from the archive.

- `-J`: This option implies that `XZ` compression is used to compress the archive. It instructs *tar* to handle the` .xz` format using the `xz` decompression tool.

- `-f tsetup.$VERSION.tar.xz`: -**f** flag is preceded by the name of the archive file that will be extracted. 

iii) Navigate to the extracted directory using the **cd** command and run the Telegram application.

```bash
 cd Telegram/
./ Telegram
```

To begin using Telegram Desktop on Ubuntu, click `Start Messaging`.

#### Step 2: Using Snap

Canonical developed the Snap system, which is used to package and install apps on Linux kernel and systemd init devices.

Install Snap using these steps if it isn't already installed on your Ubuntu system:

```bash
sudo apt update && sudo apt install snapd
```

The command below can be used to install Telegram Desktop with the Snap package:

```bash
sudo snap install telegram-desktop
```

##### Launch Telegram Desktop on Ubuntu.

After Telegram Desktop has been successfully installed on Ubuntu, open it by typing "telegram-desktop" into the command line interface or choosing Telegram Desktop from the menu, as shown below.

i) From the command line interface

```bash
telegram-desktop
```

ii) From the Desktop Environment

Go to Menu and search for “**telegram**” to launch.

iii) Click on “`Start Messaging`” to start using Telegram Desktop on Ubuntu.

![](/home/chiloba/Pictures/productivity%20Folder/Productivity-In-Everyday-Use-31.png)

The latter features of Telegram would be more interesting to users in terms of security and anonymity, or those seeking fewer restrictions compared to other messenger applications. These features are also frequently used by enterprises, communities, and content publishers to reach out to large groups of people.

### Cisco Webex

Cisco Webex is one of the leading video conferencing and collaboration platforms that assist in conducting remote communication between business entities. It provides for continuous meeting, messaging, file sharing, and screen sharing. Webex offers all-in-one video, audio, and chat to its users for unified collaboration. It is known for its high-quality video calling, security features, and holding webinars and conferences on a large scale.

Webex does have a more integrated desktop application for Linux, which includes Ubuntu, designed to enhance the general user experience of the operating system.

*Features of Cisco Webex:*

- **Video and Audio Conferencing**: (High‐performance) video and audio telephony, for example, one‐on‐one or group discussions.

- **Screen Sharing**: Share your screen with the other meeting participants to facilitate cooperation on presentations or documents.

- **Messaging**: Instant messaging and group chat both before, during, and after the meetings to guarantee everything runs smoothly.

- **File Sharing**: Easily share files in chats or during meetings.

- **Meeting Recording**: Annotate your meetings for key discussions or meetings with those who are unable to attend.

- **Virtual Backgrounds**: Convert to virtual backgrounds either to go private with your video calls or do professional virtual conferences.

- **Security**: Ensure privacy via end-to-end encryption and password-protected sessions; strengthen controls via access management policies for security.

#### Install Cisco Webex On Ubuntu System

The procedures listed below can be used to install Webex on Ubuntu. We shall demonstrate using two options, which are .`deb` package and `Snap`.

##### Option 1: Install Cisco Webex Using .deb Package

Go to the official Cisco Webex [download](https://www.webex.com/downloads.html) page and click the **"For Linux (DEB)"** button to download manually. The package can also be downloaded straight from the command line by using the wget command:

Ensure that wget is installed so that you can use it to download the file.

```bash
sudo apt update && sudo apt install wget
```

Then download the .deb package file using wget.

```bash
wget https://binaries.webex.com/WebexDesktop-Ubuntu-Official-Package/Webex.deb
```

After the download is finished, you can use` apt or dpkg` to install the <u>.deb</u> package.

1. **Using dpkg**:
   
   ```bash
   sudo dpkg -i webex.deb
   ```
   
   - The - **i** option is used to install a .deb package.

2. **Using apt:**

```bash
sudo apt install ./webex.deb
```

After completing the installation, you'll have Cisco Webex installed on your Ubuntu system. Search it in the application menu.

##### Option 2: Install Cisco Webex via Snap Package

Snap is typically pre-installed on Ubuntu systems. Run the following to confirm and install Snap if required:

```bash
sudo apt update && sudo apt install snapd
```

After Snap is configured, run the following command to install Webex:

```bash
sudo snap install webex
```

##### Launch Cisco Webex

When Webex has finished installing, you can start it by searching "**Webex**" in your application launcher or by running <u>webex</u> in the terminal:

```bash
webex
```

- After selecting the `Webex` icon, a certificate of terms and conditions will show up. Click "`Agree`" to go to the login page:

- On the welcome page you can *sign in, join a meeting, or create a new account*.

![](/home/chiloba/Pictures/productivity%20Folder/Productivity-In-Everyday-Use-30.png)

Cisco Webex is an effective and powerful collaboration platform, extending better individual and team productivity. It provides great video conferencing, instant messaging, file sharing, and screen sharing for smooth communication, allowing collaboration to take place effectively, irrespective of the location.

### Jitsi Meet

Jitsi Meet is a free and open-source platform for video conferencing. Users can create and enter conference rooms, often without the need to create an account or download software installation. Jitsi Meet is part of the larger project Jitsi, which introduces scalable video conferencing possibilities in a secure way. Access Jitsi Meet directly from within a web browser, or download iOS and Android mobile apps.

*Features of Jitsi Meet:*

The following are some awesome characteristics of Jitsi Meet.

- **Browser-Based Usage**: No need to download any program with Jitsi Meet, as it works from within modern browsers like Chrome, Edge, or Firefox.

- **Recording and Live Streaming**: One can stream meetings live to platforms such as YouTube or record and preserve them.

- **Virtual Backgrounds**: A user can change or obscure his/her background for greater privacy.

- **No Account Needed**: You can access and use the meeting without creating an account or logging in.

- **Optional End-to-End Encryption**: Jitsi Meet has imposed strong encryption to protect the privacy of users. While available, the end-to-end encryption is still experimental for certain configurations.

- **Customizable URLs**: To reach calls with ease, users are allowed to create and share unique meeting URLs.

- **Screen Sharing**: Screen sharing enables remote troubleshooting, presentations, and teamwork.

- **Unlimited Participants**: While performance depends on the server, Jitsi Meet does not really have tight participant limits like many other platforms.

- **Integrations**: It can be integrated with other programs for scheduling and notifications, which include Microsoft Outlook, Google Calendar, and Slack.

#### Install Jitsi Meet on Ubuntu System

Follow the following instructions step by step to install Jitsi Meet on an Ubuntu system.

##### Step 1: Setting the System Hostname

This step involves changing the hostname of the system to the domain name you want to use for your instance of Jitsi Meet. Additionally, that hostname will be locally resolved to the public IP of your server. When installing and creating its configuration files, Jitsi Meet makes use of both settings.  

First, configure the hostname of the system to match the domain name you plan to use for your Jitsi instance. The current hostname will be set using the following command, which will also change the `/etc/hostname` file that stores the system's hostname in between reboots:

```bash
sudo hostnamectl set-hostname jitsi.your_domain
```

 In this case we shall set our hostname to **ubuntu.cloudspinx.com**. It will look like below:

```bash
sudo hostnamectl set-hostname ubuntu.cloudspinx.com
```

When asked, enter your password. The following is an explanation of the command you executed:

- `hostnamectl`: A tool for managing the system hostname that is part of the [systemd](https://systemd.io/) tool package.

- `set-hostname`: sets the hostname for the machine.

You can now verify the hostname using the below command:

```bash
hostnamectl
```

Next, you'll make a local map of the server's hostname to its public IP address. You can do that by opening /etc/hosts with nano or your preferred text editor:  

```bash
sudo nano /etc/hosts
```

Now, you have to add the below line under `127.0.0.1 localhost`.

```bash
192.168.100.8   ubuntu.cloudspinx.com
```

For example, if your server's public IP address is `192.168.100.8`, the file would look like this after being updated:

![](/home/chiloba/Pictures/productivity%20Folder/Productivity-In-Everyday-Use-38.png)

Now your server is prepared with a hostname and IP address setting that Jitsi needs to have when installed. Save and exit the file.

##### Step 2: Configure UFW Firewall

To connect to the call participants, the Jitsi server must have a few more ports available. Additionally, a port must be open during the TLS installation procedure in order to authenticate the certificate registration request.  

In case you haven't permitted SSH traffic over UFW yet, execute the subsequent command:

```bash
sudo ufw allow OpenSSH
```

After that, let Jitsi access the following ports:  

- `80/tcp`:The port used when registering for a TLS certificate.  

- `443/tcp`:The conference room creation web page uses this port.  

- `10000/udp` `3478/udp` `5349/tcp`:The encrypted call communication will be sent and received over these ports.

Now run the belwo ufw commands to open the above ports:

```bash
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw allow 3478/udp
sudo ufw allow 5349/tcp
sudo ufw allow 10000/udp
```

Use the ufw status command to verify that they were all added:

```bash
sudo ufw status
```

The status should output active. If it's inactive, you have to **enable UFW** using the below command.

```bash
sudo ufw enable
```

Verify the status again to make sure the ports are open.

##### Step 3: Installing Jitsi Meet

Your server will now serve the Prosody APT and Jitsi repositories. Jitsi uses the open-source [XMP](https://xmpp.org/) chat server [Prosody](https://prosody.im/) for admin authentication and messaging. Next, you will install the Jitsi Meet package from its repository so that you always have the latest stable version of the plugin.

The Jitsi GPG key should first be downloaded using the curl downloading tool. If you've not installed curl, install and download the Jitsi key.

```bash
sudo apt install curl
curl https://download.jitsi.org/jitsi-key.gpg.key -o jitsi-key.gpg.key
```

The file name that will be used to store the downloaded key data is specified by the `-o` option in this command. 

Next, use the gpg command to add the GPG key to the keyring on your system:

```bash
sudo gpg --output /usr/share/keyrings/jitsi-key.gpg --dearmor jitsi-key.gpg.key
```

This `gpg` command uses `--output `to generate a file name in which to save the keyring and `--dearmor` to unpack the key into a format that APT can utilize.

A new APT sources file containing the Jitsi repository must be created in order to add it to your server. Open the below file to create a new file.

```bash
sudo nano /etc/apt/sources.list.d/jitsi-stable.list
```

Add the below line to the file.

```bash
deb [signed-by=/usr/share/keyrings/jitsi-key.gpg] https://download.jitsi.org stable/
```

Save and close the file when you're finished.

The Prosody package will then be added using the same steps. The Prosody GPG key can be downloaded by running the below command:

```bash
curl https://prosody.im/files/prosody-debian-packages.key -o prosody-debian-packages.key
```

Following that, add the key into your server's keyring:

```bash
sudo gpg --output /usr/share/keyrings/prosody-keyring.gpg --dearmor prosody-debian-packages.key
```

Then, open a fresh Prosody sources file:

```bash
sudo nano /etc/apt/sources.list.d/prosody.list
```

Add the below line into the file:

```bash
deb [signed-by=/usr/share/keyrings/prosody-keyring.gpg] http://packages.prosody.im/debian jammy main
```

The GPG keys you downloaded can now be deleted because they are no longer required:

```bash
rm jitsi-key.gpg.key prosody-debian-packages.key
```

Lastly, install the *jitsi-meet package* after performing a system update to retrieve the package list from the new repositories:

```bash
sudo apt update && sudo apt install jitsi-meet 
```

Press **y** to proceed when prompted.

When installing Jitsi Meet, you will be asked to provide the domain name you wish to use for your Jitsi Meet instance or the IP address of your machine; for example, our domain is `ubuntu.cloudspinx.com`.

![](/home/chiloba/Pictures/productivity%20Folder/Productivity-In-Everyday-Use-39.png)

The oK button can be highlighted by moving the cursor away from the hostname field using the **TAB** key. When `OK` is highlighted, press **ENTER** to submit the hostname.

A new dialog box will then appear asking you whether you want Jitsi to utilize an existing TLS certificate or create and use a self-signed one:

![](/home/chiloba/Pictures/productivity%20Folder/Productivity-in-Everyday-use-33.png)

Choose the `Generate a new self-signed certificate` option if your Jitsi domain does not currently have a TLS certificate.

Your Jitsi Meet instance is currently being configured with a self-signed TLS certificate. If you don't have a TLS certificate yet, your browser will alert you; therefore, the next step is to obtain a signed TLS certificate.

##### Step 5: Obtaining a Signed TLS Certificate

To prevent anyone from listening in on your call while it's being transmitted over the internet, Jitsi Meet encrypts the call flow using TLS certificates. Websites allow HTTPS-protected pages using the same technology, TLS certificates.  

Jitsi obtains and maintains free, safe, and industry-standard TLS certificates using the [certbot](https://certbot.eff.org/) program. Before Jitsi can obtain the necessary certificate, you must install this software.

Run the below command to install certbot.

```bas
sudo apt install certbot
```

Jitsi Meet has a script that will download a TLS certificate for your domain automatically. To start the certificate installation script that Jitsi Meet has supplied, run the following command. 

```bash
sudo /usr/share/jitsi-meet/scripts/install-letsencrypt-cert.sh
```

```bash
-------------------------------------------------------------------------
This script will:
- Need a working DNS record pointing to this machine(for hostname )
- Install additional dependencies in order to request Let’s Encrypt certificate (acme.sh)
- Configure and reload nginx or apache2, whichever is used
- Configure the coturn server to use Let's Encrypt certificate and add required deploy hooks
- Configure renew of certificate

You need to agree to the ACME server's Subscriber Agreement (https://letsencrypt.org/documents/LE-SA-v1.1.1-August-1-2016.pdf) 
by providing an email address for important account notifications
Enter your email and press [ENTER]: jitsi34@gmail.com
```

You will get notifications on security and other certificate-related issues from this email address, which will be sent to the certificate issuer, `https://letsencrypt.org`. To continue with the installation, you **must provide your email address here**.

##### Locking Conference Room Creation

You will now set up your Jitsi Meet server such that conference rooms may only be created by registered users.  

The installer created the files you will be editing and set them up with your domain name. The variable **jitsi.your_domain** will be used in place of your domain name in the examples that follow.

Open the following file with your best editor.

```bas
sudo nano /etc/prosody/conf.avail/your_domain.cfg.lua
```

Next, use nano's search feature, **CTRL+W**, to locate the line you need to alter in this file. Type **authentication = "anonymous"** into the search area after pressing **CTRL+W**. To start the search, hit **ENTER**. 

The line that needs editing will be highlighted by this search. From its existing configuration, change the following line:

```bash
   authentication = "anonymous"
```

Replace with the following setting:

```bash
  authentication = "internal_plain"
```

This setting instructs Jitsi Meet to require login and password verification before permitting a new visitor to create a conference room.

Add the subsequent section at the end of the same file:

```bash
...
VirtualHost "guest.jitsi.your_domain"
    authentication = "anonymous"
    c2s_require_encryption = false
    modules_enabled = {
            "bosh";
            "ping";
            "pubsub";
            "speakerstats";
            "turncredentials";
            "conference_duration";
    }
```

With this setup, anyone can join conference rooms created by an authenticated user. But in order to access it, the visitor needs to have the special URL (and an optional password).  

You put "**guest.**" at the beginning of your domain name here. The proper name to enter here, for instance, is `guest.jitsi.your_domain` for **jitsi.your_domain**. The guest hostname is used internally by Jitsi Meet, so you won't ever need to input it in a browser or create a separate DNS record for it.

Save and exit the file. Following that, use a text editor to open another configuration file located at ``/etc/jitsi/meet/jitsi.your_domain-config.js``:

```bash
sudo nano /etc/jitsi/meet/jitsi.your_domain-config.js
```

Search for anonymousdomain: using the keyboard shortcut CTRL+W once more. This will bring up the following line:

```bash
// anonymousdomain: 'guest.example.com',
```

Remove the two slashes // at the beginning of this line to make it look like this:

```bas
 anonymousdomain: 'guest.jitsi.your_domain',
```

For ourcase it will look like this:

```bash
anonymousdomain: 'guest.ubuntu.cloudspinx.com',
```

The `guest.jitsi.your_domain` hostname that you previously used will be used this time. This setup notifies Jitsi Meet the internal hostname requirements for guests that are not authenticated. Save and close the file.

Next, create the following file and open it with your favorite editor.

```bash
sudo nano /etc/jitsi/jicofo/sip-communicator.properties
```

Add the below line.

```bash
org.jitsi.jicofo.auth.URL=XMPP:jitsi.your_domain
```

Through this configuration, one of the Jitsi Meet processes is sent to the local server that handles the now-necessary user authentication. After finishing, save the file and close it.

As Jitsi Meet is now set up to need authorized users in order to create rooms, you must register these individuals along with their credentials. To do this, you'll utilize the `prosodyctl` tool.

Input the command provided below to add a **user**. Replace it accordingly.

```bash
sudo prosodyctl register user your_domain password
```

You added a user here, but they are not system users. They can't access your server over SSH; they can only create a conference room.

You'll see the below output from the above command.

```bash
general             warn        Lua 5.1 has several issues and support is being phased out, consider upgrading
```

The **Lua5.1** package does not present a security risk to your system and is still a necessary requirement for Prosody. When Prosody and Jitsi Meet are further developed, the reliance on Lua 5.1 will be gradually eliminated.

Lastly, to load the updated settings, restart every Jitsi Meet process by running the below command:

```bash
sudo systemctl restart prosody.service jicofo.service jitsi-videobridge2.service
```

At this point, your Jitsi Meet server is completely set up, operational, and installed. The last step will involve creating a new meeting room.

##### Step 6: Access Jitsi Meet

You are now able to access and utilize your newly created Jitsi Meet server. Enter your Jitsi domain name or IP address (with **https**) in the address bar of your browser after it has opened.

```bash
https://<your domain> or ip
```

For instance:

```bash
https://ubuntu.cloudspinx.com or https://192.168.100.8 
```

To initiate a meeting, click the landing page's "`Start Meeting`" button:

![](/home/chiloba/Pictures/productivity%20Folder/Productivity-In-Everyday-Use-35.png)

After creating a meeting, you may test this for yourself after copying the URL by clicking invite people and pasting the meeting URL into a new, incognito browser tab. You won't need a login and password to attend the meeting as a new participant.

Jitsi Meet allows for effective communication because of its intuitive design, powerful features, and flexibility. Be it remote teams, client meetings, or virtual classrooms, it saves time, reduces costs, and smoothes workflows, making it indispensable in the modern way of productivity.
![Alt text for Productivity-in-everyday-Use-10.png](Productivity-in-everyday-Use-10.png)
![Alt text for Productivity-in-Everyday-Use-10.png](Productivity-in-Everyday-Use-10.png)
![Alt text for Productivity-In-Everyday-Use-10.png](Productivity-In-Everyday-Use-10.png)
![Alt text for Productivity-in-Everyday-Use-11.png](Productivity-in-Everyday-Use-11.png)
![Alt text for Productivity-In-Everyday-Use-11.png](Productivity-In-Everyday-Use-11.png)
![Alt text for Productivity-in-Everyday-Use-12.png](Productivity-in-Everyday-Use-12.png)
![Alt text for Productivity-In-Everyday-Use-12.png](Productivity-In-Everyday-Use-12.png)
![Alt text for Productivity-in-Everyday-Use-13.png](Productivity-in-Everyday-Use-13.png)
![Alt text for Productivity-In-everyday-use-13.png](Productivity-In-everyday-use-13.png)
![Alt text for Productivity-In-Everyday-Use-13.png](Productivity-In-Everyday-Use-13.png)
![Alt text for Productivity-in-Everyday-Use-14.png](Productivity-in-Everyday-Use-14.png)
![Alt text for Productivity-In-Everyday-Use-14.png](Productivity-In-Everyday-Use-14.png)
![Alt text for Productivity-in-Everyday-Use-15.png](Productivity-in-Everyday-Use-15.png)
![Alt text for Productivity-In-Everyday-Use-15.png](Productivity-In-Everyday-Use-15.png)
![Alt text for Productivity-in-Everyday-Use-16.png](Productivity-in-Everyday-Use-16.png)
![Alt text for Productivity-In-Everyday-Use-16.png](Productivity-In-Everyday-Use-16.png)
![Alt text for Productivity-in-Everyday-Use-17.png](Productivity-in-Everyday-Use-17.png)
![Alt text for Productivity-In-Everyday-Use-17.png](Productivity-In-Everyday-Use-17.png)
![Alt text for Productivity-in-Everyday-Use-18.png](Productivity-in-Everyday-Use-18.png)
![Alt text for Productivity-In-Everyday-Use-18.png](Productivity-In-Everyday-Use-18.png)
![Alt text for Productivity-in-Everyday-Use-19.png](Productivity-in-Everyday-Use-19.png)
![Alt text for Productivity-In-Everyday-Use-19.png](Productivity-In-Everyday-Use-19.png)
![Alt text for productivity-in-everyday-use-1.png](productivity-in-everyday-use-1.png)
![Alt text for Productivity-in-Everyday-Use-1.png](Productivity-in-Everyday-Use-1.png)
![Alt text for Productivity-In-Everyday-Use-1.png](Productivity-In-Everyday-Use-1.png)
![Alt text for Productivity-in-Everyday-Use-20.png](Productivity-in-Everyday-Use-20.png)
![Alt text for Productivity-In-Everyday-Use-20.png](Productivity-In-Everyday-Use-20.png)
![Alt text for Productivity-in-Everyday-Use-21.png](Productivity-in-Everyday-Use-21.png)
![Alt text for Productivity-In-Everyday-use-21.png](Productivity-In-Everyday-use-21.png)
![Alt text for Productivity-In-Everyday-Use-21.png](Productivity-In-Everyday-Use-21.png)
![Alt text for productivity-in-everyday-use-2 (1).png](productivity-in-everyday-use-2 (1).png)
![Alt text for Productivity-In-Everyday-use-22.png](Productivity-In-Everyday-use-22.png)
![Alt text for Productivity-In-Everyday-Use-22.png](Productivity-In-Everyday-Use-22.png)
![Alt text for Productivity-in-Everyday-Use-23.png](Productivity-in-Everyday-Use-23.png)
![Alt text for Productivity-In-Everyday-Use-23.png](Productivity-In-Everyday-Use-23.png)
![Alt text for Productivity-In-Everyday-Use-24.png](Productivity-In-Everyday-Use-24.png)
![Alt text for Productivity-In-Everyday-Use-25.png](Productivity-In-Everyday-Use-25.png)
![Alt text for Productivity-in-Everyday-use-26.png](Productivity-in-Everyday-use-26.png)
![Alt text for Productivity-In-Everyday-Use-26.png](Productivity-In-Everyday-Use-26.png)
![Alt text for Productivity-In-Everyday-Use-27.png](Productivity-In-Everyday-Use-27.png)
![Alt text for Productivity-In-Everyday-Use-28.png](Productivity-In-Everyday-Use-28.png)
![Alt text for Productivity-In-Everyday-Use-29.png](Productivity-In-Everyday-Use-29.png)
![Alt text for productivity-in-everyday-use-2.png](productivity-in-everyday-use-2.png)
![Alt text for productivity-in-everyday-Use-2.png](productivity-in-everyday-Use-2.png)
![Alt text for Productivity-In-Everyday-Use-2.png](Productivity-In-Everyday-Use-2.png)
![Alt text for Productivity-In-Everyday-Use-30.png](Productivity-In-Everyday-Use-30.png)
![Alt text for Productivity-In-Everyday-Use-31.png](Productivity-In-Everyday-Use-31.png)
![Alt text for Productivity-In-Everyday-use-32.png](Productivity-In-Everyday-use-32.png)
![Alt text for Productivity-In-Everyday-Use-32.png](Productivity-In-Everyday-Use-32.png)
![Alt text for Productivity-in-Everyday-use-33.png](Productivity-in-Everyday-use-33.png)
![Alt text for Productivity-In-Everyday-Use-33.png](Productivity-In-Everyday-Use-33.png)
![Alt text for Productivity-In-Everyday-Use-34.png](Productivity-In-Everyday-Use-34.png)
![Alt text for Productivity-In-Everyday-Use-35.png](Productivity-In-Everyday-Use-35.png)
![Alt text for Productivity-In-Everyday-Use-36.png](Productivity-In-Everyday-Use-36.png)
![Alt text for Productivity-In-Everyday-Use-37.png](Productivity-In-Everyday-Use-37.png)
![Alt text for Productivity-In-Everyday-Use-38.png](Productivity-In-Everyday-Use-38.png)
![Alt text for Productivity-In-Everyday-Use-39.png](Productivity-In-Everyday-Use-39.png)
![Alt text for productivity-in-everyday-use-3.png](productivity-in-everyday-use-3.png)
![Alt text for Productivity-In-Everyday-Use-3.png](Productivity-In-Everyday-Use-3.png)
![Alt text for productivity-in-everyday-use-4.png](productivity-in-everyday-use-4.png)
![Alt text for Productivity-In-Everyday-Use-4.png](Productivity-In-Everyday-Use-4.png)
![Alt text for Productivity-In-Everyday-Use-5.png](Productivity-In-Everyday-Use-5.png)
![Alt text for Productivity-In-Everyday-Use-6.png](Productivity-In-Everyday-Use-6.png)
![Alt text for Productivity-in-Everyday-Use-7.png](Productivity-in-Everyday-Use-7.png)
![Alt text for Productivity-In-Everyday-Use-7.png](Productivity-In-Everyday-Use-7.png)
![Alt text for Productivity-in-Everyday-Use-8.png](Productivity-in-Everyday-Use-8.png)
![Alt text for Productivity-In-Everyday-Use-8.png](Productivity-In-Everyday-Use-8.png)
![Alt text for Productivity-in-Everyday-Use-9.png](Productivity-in-Everyday-Use-9.png)
![Alt text for Productivity-In-Everyday-Use-9.png](Productivity-In-Everyday-Use-9.png)
![Alt text for Productivity-in-Everyday-Use.png](Productivity-in-Everyday-Use.png)
![Alt text for Productivity-In-Everyday-Use.png](Productivity-In-Everyday-Use.png)
