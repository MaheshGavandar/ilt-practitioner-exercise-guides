# Lab 1.1: Login welcome page

All accounts needed for the labs in this course have credentials displayed on
the classroom welcome page.

.callout.info Your instructor will provide you with a 4 digit class id. Replace the `XXXX` in
these instructions with that ID.

Using your computer login to `https://classXXXX.classroom.puppet.com`

You will be prompted for an email address. Your instructor will assign
you a student number. Replace the `N` with the student number provided in
these instructions with that number.

Login with `studentN@puppet.com` e.g. `student0@puppet.com.`

> When you've completed a Lab or an Exercise, please check off the
> *Activity complete* button if you see it. Your slides will not advance along with
> the instructor's until you do so.

## Steps:

.callout.info Requirements: An SSH client such as Terminal.app or iTerm2.app, or optionally Microsoft Remote Desktop ( can be found preinstalled on Windows and in the macOS AppStore.)

> For macOS use Microsoft Remote Desktop version 10 and higher

### Logging into Linux Using macOS or Linux

You have the choice of logging into Linux directly form your computer or using
the Remote Desktop Connection to "jump" to the Linux box using the PuTTY
terminal emulation software on Windows. If your laptop is on Windows, follow
the instructions above to the "jump" host as they both will involve using PuTTY
on Windows.

#### Linux or macOS

From the Welcome page download the "student.pem" private key file. Note where
it is located as you will use it as the value of an argument below.

.callout.info Do not use the `private_key.ppk` file, this file is formatted for the windows PuTTY application.

Using a terminal (Terminal.app, Konsol) type

    @@@ Console nochrome
    chmod 600 /path/to/downloaded/student.pem

    ssh centos@XXXXnixN.classroom.puppet.com -i /path/to/downloaded/student.pem

> Tip you can type `-i` and drag the file into the Terminal window in most
> applications , to automatically fill the path to the file in.

.callout.notice Proceed to the Validate and configure the agent environment

## __Optional__ Logging into Linux via Windows

.callout.info The labs will be done on Linux in this course. The Windows workstation is there as a convenience should you prefer to use it.

Using the username "Administrator" and the __windows__ "RDP Password" displayed
to you on the welcome page, connect to the "hostname" displayed on the welcome
page under "Type: Windows".

> If you prompted about the security of the certificate , acknowledge the dialog
> affirmatively e.g. "continue". The certificates used in this classroom are
> self signed and will not be trusted by your operating system by default.

### Connecting to the Linux Host using PuTTY or Openssh method

.callout.terminal If you would like to connect directly from your macOS or Linux
workstation skip these steps and proceed to the optional steps below.

#### PuTTY Method
1. On your Windows student machine, open a PowerShell window
1. Launch PuTTY by typing `putty` and pressing enter:
    * In the Host Name field, copy and paste your Linux machine's hostname from the Welcome page
    * On the left hand menu, expand `SSH` and click on **Auth**
        * Under `Private key file for authentication`, click the **Browse** button
        * Select the pre-loaded private key from `C:\keys`.
        * Select **private_key.ppk** and click **Open**
    * Next, under the `Connection` category, click on **Data**
        * In the `Auto-login username` field, type **centos**
    * Return to the session view by clicking **Session** on the left-hand menu in PuTTY
    * In the `Saved Sessions` box, type in **linux_machine** and click **Save** on the right hand side
    * Click **Open**
        * If prompted about the host key not being cached, select **Yes**

.callout.info For any future connections to this host, you can now simply double-click **linux_machine** in the `Saved Sessions` window

#### OpenSSH method

1. On your Windows student machine, open a PowerShell window
1. Install win32-openssh using chocolatey, `choco install openssh` and press enter:
    * When the install is done, restart PowerShell
    * You can then use the credentials already on the host
1. Re-open PowerShell and type in `ssh centos@<your-linux-machine>.classroom.puppet.com`

### Validate and configure the agent environment

Verify that Git is installed. You will use this for version control when you edit Puppet code.

.callout.thumbsup You should see output similar to the following (note: your version number may be different):

    @@@ Console nochrome
    [centos@XXXXlinN ~]$ git --version
    git version 1.8.3.1

.callout.info For all labs in this class, `sudo su -` so that you are root. All labs are to be completed as root

### Install the Puppet agent using Bolt:

### Step 1

Execute the following commands to add the required YUM repository and install the bolt package:

    @@@ Console nochrome
    sudo rpm -Uvh https://yum.puppet.com/puppet5/puppet5-release-el-7.noarch.rpm
    sudo yum install -y puppet-bolt

### Step 2

Now you will validate if your bolt installation is working properly:

    @@@ Console nochrome
    $ bolt --version
    0.21.3

### Step 3

A basic installation script has been pre-staged in your home directory, here `~/install_pe_agent.sh`

Invoke the script using Bolt in order to install the agent on your local system:

    @@@ Console code_wrap nochrome
    [centos@XXXXlinN ~]$ sudo /usr/local/bin/bolt script run install_pe_agent.sh --nodes localhost

### Explore your new puppet agent installation

1. Run the following commands:
    * `puppet --version`
    * `puppet agent --configprint confdir`
    * `puppet agent --configprint certname`
    * `puppet agent --configprint server`
1. Experiment with the management tools.
    * Services
      * `systemctl status crond`
    * Users
      * `useradd marypoppins`
      * `id marypoppins`
    * Packages
      * `yum install tree`
      * `yum info tree`

### Mark the activity complete

1. Return to the presentation in your web browser.
1. Check off the *Activity complete* button if you see it.

1. [Lab 2.1 Editing Code](Lab 02.1 Editing code)