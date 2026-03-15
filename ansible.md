 **ANSIBLE https://docs.ansible.com**

Ansible is called agentless, which means that there is no need to install any additional software on the target machines to be able to work with ansible. A simple SSH connectivity would suffice ansible’s needs.

Ansible helps to increase productivity and efficiency by automating a lot of repetitive tasks in the environment. Whether it be sizing and creating new hosts or VM’s, applying configurations on them, patching hundreds of servers, migrations, deploying applications or even performing security and compliance audits. Ansible is a powerful IT automation tool. YAML, which is the language of ansible.

All ansible playbooks are written in YAML.

Configuration Management is **the process of maintaining systems, such as computer hardware and software, in a desired state**. Configuration Management (CM) is also a method of ensuring that systems perform in a manner consistent with expectations over time.

Ansible will access AWS resources using boto SDK.

**What Ansible is** -

If you're a systems engineer or IT administrator, just anybody working in IT, you're probably involved in doing a lot of repetitive tasks in your environment. Whether it be sizing, creating new hosts, virtual machines every day, finding configurations on them, patching on hundreds of servers, migrations, deploying applications, even performing security compliance audits. All of these very repetitive tasks involve execution of hundreds of commands on hundreds of different servers while maintaining the right sequence of events, with system reboots that are not in between. Some people develop scripts to automate these tasks that require coding skills and regular maintenance of these scripts, and a lot of time to put these scripts together in the first place. That's where Ansible helps.

Ansible is a powerful IT automation tool, used to automate even the most complex deployments.

**Example:**

Let's take a look at a simple use case. Imagine you have a number of hosts in our environment that you would like to restart in a particular order. Some of them are web servers, others are database servers. You would like to power down the web servers first, followed by the database servers, then power up the database servers, then the web servers. You could write an Ansible playbook to get this done in a matter of minutes, and simply invoke the Ansible playbook every time you wish to restart your application

**Ansible inventory**

Ansible can work with one or multiple systems in the infrastructure at the same time. In order to work with multiple servers, ansible needs to establish connectivity to those servers, this is done using SSH for linux and powershell remoting for windows.  
Ansible is called agentless, which means that there is no need to install any additional software on the target machines to be able to work with ansible. A simple SSH connectivity would suffice ansible’s needs.**Inventory file - /etc/ansible/hosts**

![](images/media/image45.png)

![](images/media/image38.png)

Ansible\_host is an inventory parameter used to specify the FQDN or IP address of a server, other inventory parameters include – ansible\_connection, ansible\_port.

Ansible configuration file 🡪 vi /etc/ansible/ansible.cfg

**Ansible playbooks**

Ansible playbooks are Ansible's orchestration language. It is in playbooks where we define what we want Ansible to do, it is a set of instructions to ansible. Playbooks are text files or configuration files that are written in a particular format called YAML.

**Example:**

![](images/media/image22.png)

A playbook is a single YAML file containing a set of plays. A play defines a set of activities to be run on a single or a group of hosts. The YAML format is key while developing playbooks.  
A task is a single action to be performed on a host. Some examples of a task are executing a command or a script on the host, installing a package on the host, performing a shutdown or a restart operation. A task is a list or an array, so the order matters.  
The playbook is a list of dictionaries in YAML terms. Each play is a dictionary and has a set of properties called name, hosts, and tasks.

Playbook contains plays  
Plays contains tasks  
Tasks contain modules

**Hosts**

The host parameter indicates which hosts the operations in the YAML file to be run on.

**Ansible playbooks are idempotent as they won’t repeat the task if it already existed, whereas scripts repeat the task, with the number of times it is executed**.

![](images/media/image26.png)

**Modules**

There are over 1000 modules provided by ansible to automate every part of the environment. Modules are like plugins that do the actual work in ansible, they are what gets executed in each playbook task. Each module is mostly standalone and can be written in a standard scripting language (such as python, perl, ruby, bash, etc.). **One of the guiding properties of modules is idempotency. The different actions run by tasks are called modules.**

![](images/media/image3.png)

Ansible modules are categorized into various groups based on their functionality. Some of them are listed here,

System, commands, files, database, cloud, windows and more, there are a lot more and a comprehensive list can be found at docs.ansible.com.

System modules are actions to be performed at a system level such as modifying the users and groups on the system, modifying iptables, firewall configurations on the system, working with logical volume groups, mounting operations or working with services(for example, starting, stopping, or restarting services in a system).

Command modules are used to execute commands or scripts on a host, this could be simple commands. shell and command modules are similar in that they are used to execute a command on the system. However shell executes the command inside a shell giving us access to environment variables and redirection using \>\>

![](images/media/image12.png)

Some modules accept free-form input, and the other modules accept parameterized input, i.e., key value pair input.

![](images/media/image8.png)

We run ansible in 2 ways, first using the ansible command and then using the ansible playbook command.

**Ansible variables**

Just like any other scripting or programming language, variables are used to store values that vary with different items.  
Variables are used to store values that vary with different items. For example, let's say we are trying to perform the same operation of applying patches to hundreds of servers. We only need a single playbook for all 100 servers. However, it's the variables that store information about the different host names, usernames or passwords that are different for each server.

![](images/media/image20.png)

![](images/media/image1.png)

![](images/media/image16.png)

**Ansible conditionals**

![](images/media/image48.png)

Ansible\_os\_family is a built in variable, that ansible populates with the flavour of OS.

![](images/media/image44.png)

![](images/media/image18.png)

![](images/media/image46.png)

To record the output of one task, we could use the register directive, we say the register the output to the desired variable.

**Ansible loops**  
Loop is a looping directive that executes the same task multiple times. Loop and with\_items are both similar. ‘item’ is the default variable

![](images/media/image31.png)

![](images/media/image40.png)

![](images/media/image36.png)

![](images/media/image32.png)

**Ansible roles**

Ansible roles, logically breaks the playbook into reusable components. The primary purpose of roles is to make the work reusable. Be it for other tasks or projects within your organization or outside for others globally. Roles help us organize the project in a standard structure. Instead of all of them rewriting the same piece of code, we could package it into a role and reuse it later, next time, we could simply assign the role created. Example: MySQL (below).

![](images/media/image47.png)

![](images/media/image49.png)

All tasks into a task directory, all variables used by these tasks are stored in the vars directory, any default values go into the defaults directory, all handlers go into the handlers directory, any templates used by the playbooks go into the templates directory.

Roles also help in sharing the code with others in the ansible community, ansible galaxy is one such community, where we can find 1000’s of roles for almost any task we want.

Note: 1. Handlers folder is used to start the services. 2. /etc/ansible/roles is the default location where ansible searches for roles.

![](images/media/image43.png)

![](images/media/image30.png)

**Ansible patterns:**

We know how to define what hosts we run tasks against, patterns in ansible are how we decide which hosts to manage.  
Example: to run on multiple servers  
\- host1, host2, host3  
\- Group1, host1  
\- host\*  
\- \*.company.com

**Dynamic Inventory:**

We have seen inventory information defined in inventory files(sample inventory file). But it is not necessary to always define the inventory information in these files, because this is a static file and we have to change that manually. If we were to integrate ansible with any other source of inventory in our environment, then we will need to make this inventory dynamic. Ansible supports having dynamic inventory files, typically in ansible, we specify the input file using the ‘–i’ parameter. For dynamic inventory, instead of specifying a file, we specify a script, in the below example, it is a python script.

![C:\\Downloads\\IMG\_1486.jpg](images/media/image39.jpg)

**Institute**

![C:\\Downloads\\IMG\_1492.jpg](images/media/image27.jpg)

Setting up of servers using the keygen

Cd .ssh

Ls

Authorized\_keys (pem key will be stored) – along with this we also need one public key to authenticate other servers.

To generate public key – ssh-keygen

![C:\\Downloads\\IMG\_1501.jpg](images/media/image34.jpg)

Paste the id\_rsa.pub key in the other server in the authorized key file to authenticate.

**To authenticate other servers**

First update the internal repository and install python and ansible. Ansible is python dependent.

Vi /etc/ssh/sshd\_config

> \#Permitrootlogin – remove \# to enable

Password authentication – change it to yes

Service sshd restart

To check connection established from ansible server to other :

ssh root@ipaddroftheserver

To come out of the server – exit

**Inventory groups**

Cd /etc/ansible

Vi hosts

Create groups \[dev\], \[prod\], \[qa\] with ip address

**Ansible vault**

Ansible vault is a feature of ansible that allows you to store sensible info, such as passwords, keys and API’s in encrypted format. To protect the playbooks we use vaulting.

![C:\\Downloads\\IMG\_1526.jpg](images/media/image35.jpg)

**Ansible reusable scripts / playbooks**

Ansible modules

Module index

Choose the type of module required

Ansible galaxy

Search what is required

Go to github-repo

Tasks

Main.yml

**Udemy Advanced**

**File separation**

It is better to define the variables in a separate file for that server, instead defining it in the same inventory file. To achieve this, we first create a host\_vars directory next to the playbook and then create a file with the same name as that of the server. Then we move the variables and their values from the inventory file to the newly created file.

![C:\\Downloads\\IMG\_1511.jpg](images/media/image42.jpg)

**INCLUDE STATEMENT**

In our case we have a playbook with two sets of tasks one to install and configure the database and the other is to install and configure the web server. What if we need to reuse these tasks in different playbooks where the requirement may be to only install databases or to only install the web server. So we divide these tasks into two sets. We first create two files under a folder called Tasks naming them deploy\_db.yml and deploy\_web.yml, and we move the db tasks into the first one and the web tasks into the second one. Once we're done with that we add the include statements and under task in our playbook to include the task from these external files.

![C:\\Downloads\\IMG\_1512.jpg](images/media/image6.jpg)

**Ansible roles**

Now that we have worked with includes and variables, developing a role should be easy for us. Roles are the recommended way of developing a playbook in Ansible. rRoles help us organize our project in a standard structure. We use roles within our project and share our work with open communities through GitHub or Ansible galaxy. So what exactly does organized mean. wWhen you create a role., It automatically creates this folder structure for you that contains a set of folders like tasks, handlers, vars, defaults etc. and the readme file is initialized automatically. This will help in creating the role as per best practice. Once roles are created it is easy to use them in any part of your playbook. Simply use the roles directive to assign a role to a server. When you do this, Ansible automatically loads all the tasks from the task folder. All the variables from the variables folder and defaults from the default folder and makes them available to the playbook. You don't have to use any include commands in the main playbook. If you're using roles. This way, our main playbook looks very very simple and readable and we can reuse the same role in different parts of the playbook the same way. With Ansible Galaxy., these rules can be shared and others can import and reuse them with great ease. There are thousands of roles already available on ansible galaxy and it's a good idea to check for an existing role before starting to double up one on your own. What we have so far are the tiles separated into two task files called deploy db and deploy web. What we really want to be doing is to use roles. So our work becomes reusable. Creating two separate roles for db and web instead of a single one will help us modularize our work and will help us use each of these for different purposes in the future. If somebody only wanted to deploy a db server or a web server then this design will help us reuse our work for different purposes. So we create two separate roles called mysql\_db and flask web using the ansible galaxy in its command. Now remember we don't necessarily have to use the Ansible Galaxy in its command. We could simply create the folder structure ourselves. Ansible Galaxy command simply makes it easy for us and automatically creates the required structure. Once the roles are created and we have added all the tasks it's really easy to integrate the roles into our playbook. Instead of tasks, this time we will use roles and will simply list the name of the role that we created. In this case mysql\_db and flask\_web.

![C:\\Downloads\\IMG\_2949.jpg](images/media/image7.jpg)

![C:\\Downloads\\IMG\_2950.jpg](images/media/image25.jpg)

![C:\\Downloads\\IMG\_2951.jpg](images/media/image21.jpg)

Our application has been monolithic until now meaning both database and web application have been on the same server so far. Now that we have roles it is easy for us to change our design into a distributed application model. We would like to distribute the database and web server to two separate servers. Our new playbook looks simple too. Now we have two plays as we have two servers. The first play configures the database on the first server and the second play configures the web server on the second server<span class="underline">.</span>

**Asynchronous actions**

As it is known, ansible establishes connectivity to target servers over SSH, this means the SSH connections stay alive throughout the execution of the task in a playbook. At times, we may want to execute a long running task or a process that exceeds the SSH timeout or we may simply not want the SSH connection to stay alive throughout the operation. Instead invoke the process and check on it at a later time. Or we may want to run multiple processes at once and check on them later. Or another use case may be to run one or more processes and not even bother to check their status. All of these can be achieved using asynchronous actions.

![C:\\Downloads\\IMG\_1515.jpg](images/media/image33.jpg)

![C:\\Downloads\\IMG\_1514.jpg](images/media/image23.jpg)

Async directive is to specify the maximum time, we would expect the task to execute, how frequently does ansible check the status of the script, by default ansible every 10 seconds. If you want to change that, use the poll directive.

**Strategy**

Strategy defines how a playbook is executed in ansible

![C:\\Downloads\\IMG\_1517.jpg](images/media/image29.jpg)

It installs all the tasks mentioned, on all the servers parallely. This is called linear strategy and is the default.

![C:\\Downloads\\IMG\_1518.jpg](images/media/image24.jpg)

In this case, each server runs all of its tasks, independent of the other server and does not wait for the task to finish on the other servers.

![C:\\Downloads\\IMG\_1519.jpg](images/media/image19.jpg)

In this case, ansible executes, based on the number or the % of servers mentioned in the serial directive in the play.

Serial:

\-2

\-3

\-5

To run the play against 2 servers first, 3 next and then 5, this is mostly useful for rolling updates.

**Forks**

  - > How many servers can ansible talk to at a time, can ansible deploy the tasks on all mentioned servers (if there are 100) at a time, the answer is no, unless specified explicitly. Ansible uses parallel processes or forks to communicate with remote hosts, **ansible can create 5 forks** at a time and this is defined in the ansible configuration file ansible.cfg, this means that even if you try to run this playbook against a 100 hosts, ansible will only run across 5 at a time.

![C:\\Downloads\\IMG\_1520.jpg](images/media/image28.jpg)

By default ansible can create 5 forks at a time, that is defined in the ansible configuration file. i.e., ansible.cfg

**Error handling**

Ansible executes each task against the server, until all of them are complete. In a single server scenario, if it fails at a particular step, it straightforward exits the playbook. If the playbook is running against 3 separate servers, if it fails at a particular step, ansible takes that server out of the list and continues to execute the remainder of the tasks across the other healthy and available servers, this is the default behavior of the ansible.

By using any\_errors\_fatal=true, if any task fails on one server, ansible stops the execution of the play on all the available servers and exits.

![C:\\Downloads\\IMG\_1521.jpg](images/media/image14.jpg)

**Ignore errors, failed\_when**

At the end of our application playbook. We would like to add a new task to send out a notification email stating that the web server is ready. We use the mail module to send out an email to our team with the subject and body. In this case we are sending an email to devops@corp.com with the subject that the server is deployed and every simple body. However this is not a critical requirement and our SMTP server is not very stable. So we really don't care if this task completes successfully or not. Even if the mail doesn't go through at times we're still OK and we don't want the playbook to fail because of it. It's just good to have features. To ignore errors we could simply set **ignore\_errors** to yes on the task. Then the playbook execution will not stop and fail. Instead it will simply ignore the error and continue. Next we would like to do some error checking. For example we would like to check the contents of a file called server.log and fail the playbook if it has any errors in it. For this, we use the command module to execute a cat /var/log/server.log command. This command returns the contents of the file. As long as the file is present and readable the task will complete successfully. However, as discussed we would like to fail the playbook in case there are errors inside the file. For this we are first going to register the result of the command in a variable called command\_output and then we're going to use the failed\_when directive. We will write a condition in it to look for the word error in the command output. If it exists ansible will fail the play because the value of failed\_when will then be true. If it doesn't exist, then the value in failed\_when will be false and so it just continues as normal<span class="underline">.</span>

![C:\\Downloads\\IMG\_2645.jpg](images/media/image11.jpg)

**Jinja2 templating**

{{ }} = JINJA2 templating

{%%} = JINJA2 templating

![C:\\Downloads\\IMG\_1522.jpg](images/media/image5.jpg)

![C:\\Downloads\\IMG\_1523.jpg](images/media/image17.jpg)

![C:\\Downloads\\IMG\_1524.jpg](images/media/image4.jpg)

**Lookups 🡪** So far we've been storing credentials for our targets servers inside the inventory file. What if there are too many servers or this information is already available elsewhere. Let's say we have the credentials of the servers stored in a CSV file in a host name and password format. The first column being the host name and the second column being the password. To read the contents of the file while ansible playbook is running and to get the password associated with a host, we can use the Lookup plugin. This is how we use the Lookup plugin. For example, in this case the first argument that we passed to the LookUp plugin is the type of the file which happens to be a CSV file in this case. There are a number of other options available that we'll see in a bit. Then comes the value to lookup. For example, here we like to look up information about the server Target1, followed by the file we are looking at. For example, in this case the file is stored under the tmp directory and is called credentials.csv. And finally the Delimiter which happens to be comma(,) in this case because it's a CSV file. If you have a file which uses another separator maybe like a semicolon or something then you could specify that here. So this same lookup plugin for CSV file supports multiple other characters, separated file formats as well. In this case, this whole function or plugin is going to return the password from the CSV file. There are a few other lookup plugins available such as INI, DNS, MongoDB, etc.

**  
Lookup plugins are just like custom scripts that can do specific tasks like read files, connect to a URL, connect to a database**.

![C:\\Downloads\\IMG\_1525.jpg](images/media/image9.jpg)

**Dynamic inventory**

The dynamic inventory is inventory information that ansible retrieves programmatically when the ansible playbook is run as opposed to us defining it in a static inventory text file.

![C:\\Downloads\\IMG\_1527.jpg](images/media/image10.jpg)

![C:\\Downloads\\IMG\_1528.jpg](images/media/image2.jpg)

![C:\\Downloads\\IMG\_1529 (1).jpg](images/media/image15.jpg)

**Custom modules**

In order to develop a custom module, we have to develop a custom python script

**Commands**:

To check the connectivity with other server – ansible targetservername –m ping –I inventoryfilename

To execute ansible playbook – ansible-playbook playbookname.yml

To know more about playbook – ansible-playbook - - help

To ping target servers using ansible command – ansible all –m ping –I filename

To ping target servers using ansible playbook command – ansible-playbook playbookname.yml –I inventoryfilename

To create role – ansible-galaxy init rolename (Example: mysql)

To search roles – ansible-galaxy search rolename

To install the role – ansible-galaxy install rolename

To view the list of roles currently installed – ansible-galaxy list

To view the location where roles would be installed – ansible-config dump | grep role

To install roles in the current directory – ansible-galaxy install rolename –p ./roles

To ping server which is stored in inventory group – ansible –m ping servername

To ping all servers together – ansible –m ping all

To check if there are any syntax errors in yaml file –  
ansible-playbook playbookname.yml --syntax-check

To create a log file & move the output to the log file –  
ansible\_playbook playbookname.yml \>\> filename.log

To create a vault file – ansible-vault create filename.txt

To edit the content in vault file – ansible-vault edit filename

To view the vault file – ansible-vault view filename

To change the password of vault file – ansible-vault rekey filename

To decrypt the file – ansible-vault decrypt filename

To add vault for existing file – ansible-vault encrypt filename or playbookname.yml

If encrypted file is used in the project then we must append the option ask-vault-pass, so that the ansible asks for the vault password - ansible-playbook playbookname.yml –I inventoryfilename –ask-vault-pass

**<span class="underline">Introduction to Ansible Configuration files in Udemy</span>**

When Ansible is installed, it creates a default configuration file at the location, **/etc/ansible/ansible.cfg.** The Ansible configuration file governs the default behavior of Ansible using a set of parameters.

![](images/media/image41.png)

Here, different ways of specifying the configuration file have been mentioned. What if all of them have been configured and different values for different parameters in each of them? which one does it consider, and what order does ansible pick the configuration files in?

1.  > First priority is always to the parameters configured in the file specified through an environment variable. Any values configured in this file overrides the values configured in all other files.

2.  > ansible.cfg in the current directory.

3.  > .ansible.cfg file in the user’s home directory.

4.  > default configuration file in /etc/ansible/ansible.cfg

![](images/media/image13.png)![](images/media/image37.png)
