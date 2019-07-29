# ANSIBLE ARCHITECTURE

![logo](https://3.bp.blogspot.com/-tC1S8lMBm3Y/V47kVwG2B3I/AAAAAAAAAwY/Xz2UJP9wwJIs0t-QJofhJl_DZcdTYjIzgCLcB/s1600/ANSIBLE_DIAGRAM.jpg)

# Ansible components
## 1.Inventory
- The “inventory” is a configuration file where you define the host information(or) File containing data about the ansible client servers.
- In the above /etc/ansible/hosts example, we declared two servers under test-hosts.

## 2.Playbooks
- In most cases – especially in enterprise environments – you should use Ansible playbooks. A playbook is where you define how to apply - policies, declare configurations, orchestrate steps and launch tasks either synchronously or asynchronously on your servers. Each - --- playbook is composed of one or more “plays”. Playbooks are normally maintained and managed in a version control system like Git. They - are expressed in YAML (Yet Another Markup Language).
### Plays
- Playbooks contain plays. Plays are essentially groups of tasks that are performed on defined hosts to enforce your defined functions. - Each play must specify a host or group of hosts. For example, using:
 ``` – hosts: all ```
- …we specify all hosts. Note that YML files are very sensitive to white spaces, so be careful!

## 3.Tasks
- Tasks are actions carried out by playbooks(or)A task is a section that consists of a single procedure to be completed .
-  One example of a task in an Apache playbook is:
``` - name: Install Apache httpd ```
- A task definition can contain modules such as yum, git, service, and copy.

## 4. Modules
- Ansible connects your nodes and pushes out the small “Ansible Modules” programs. Modules are being executed by the Ansible and then - - get removed when finished. These modules can reside on any machine, no servers or daemons or databases are required here. You can - --- work with text editor of your choice or a terminal and a version control system to keep track of the changes made in your content.

## 5. Plugins
- Piece of code which expands the core functionality of Ansible. There are plenty of handy plugins and you can write your own too.

## 6. API’s
- Ansible API’s works as a transport for the Cloud Services, public or private.

## 7. Hosts 
- Hosts are basically node systems in the Ansible Architecture getting automated by Ansible only, any type of machine like- Windows, - -RedHat, Linux, etc.

## 8. Networking
- We can also use Ansible to automate different networks, it uses the easy, simple and yet powerful agentless automation framework for IT operations and development. It uses a type of data model (playbook or role) which is separated from the Ansible Automation Engine that spans the different network hardware quite easily.

## 9. CMDB
- A type of repository which acts as a data warehouse for the IT installations.
## 10. Cloud 
- A network of remote servers on which you can store, manage and process your data, these servers are hosted on internet, storing the data remotely rather than local servers, just launch your resources and instances on cloud, connect them to your servers and you’ve the wisdom of operating your task remotely.

# Examples
```
1)display username
$ Ansible test-servers -a “/sbin/reboot” -f 10 -u username
2)File transfer
$ Ansible test-servers -m copy -a “src = /etc/yum.conf dest = /tmp/yum.conf” 
3) Create new directory
$ Ansible test-servers -m file -a “dest = /path/user1/new mode = 777 owner = user1 group = user1 state = directory”
4) Delete files or directories
$ Ansible test-servers -m file -a “dest = /path/user1/new state = absent”
5)Check package installed  or not
$ Ansible test-servers -m yum -a “name = demo-tomcat-1 state = present”
$ Ansible test-servers -m yum -a “name = demo-tomcat-1 state = absent”
$ Ansible test-servers -m yum -a “name = demo-tomcat-1 state = latest”
6) To get all facts
$ Ansible all -m setup

```










# ansible
- https://www.softwaretestinghelp.com/ansible-roles-jenkins-integration-ec2-modules/
- https://foxutech.com/how-to-run-a-ansible-playbook-using-jenkins/
- https://docs.ansible.com/ansible/latest/modules/aws_region_facts_module.html ---for aws ec2 instance creation
- https://docs.aws.amazon.com/general/latest/gr/rande.html#ec2_region aws regions
## ansible usage
```
Usage: ansible <host-pattern> [options]

Define and run a single task 'playbook' against a set of hosts

Options:
  -a MODULE_ARGS, --args=MODULE_ARGS
                        module arguments
  --ask-vault-pass      ask for vault password
  -B SECONDS, --background=SECONDS
                        run asynchronously, failing after X seconds
                        (default=N/A)
  -C, --check           don't make any changes; instead, try to predict some
                        of the changes that may occur
  -D, --diff            when changing (small) files and templates, show the
                        differences in those files; works great with --check
  -e EXTRA_VARS, --extra-vars=EXTRA_VARS
                        set additional variables as key=value or YAML/JSON, if
                        filename prepend with @
  -f FORKS, --forks=FORKS
                        specify number of parallel processes to use
                        (default=5)
  -h, --help            show this help message and exit
  -i INVENTORY, --inventory=INVENTORY, --inventory-file=INVENTORY
                        specify inventory host path or comma separated host
                        list. --inventory-file is deprecated
  -l SUBSET, --limit=SUBSET
                        further limit selected hosts to an additional pattern
  --list-hosts          outputs a list of matching hosts; does not execute
                        anything else
  -m MODULE_NAME, --module-name=MODULE_NAME
                        module name to execute (default=command)
  -M MODULE_PATH, --module-path=MODULE_PATH
                        prepend colon-separated path(s) to module library (def
                        ault=~/.ansible/plugins/modules:/usr/share/ansible/plu
                        gins/modules)
  -o, --one-line        condense output
  --playbook-dir=BASEDIR
                        Since this tool does not use playbooks, use this as a
                        substitute playbook directory.This sets the relative
                        path for many features including roles/ group_vars/
                        etc.
  -P POLL_INTERVAL, --poll=POLL_INTERVAL
                        set the poll interval if using -B (default=15)
  --syntax-check        perform a syntax check on the playbook, but do not
                        execute it
  -t TREE, --tree=TREE  log output to this directory
  --vault-id=VAULT_IDS  the vault identity to use
  --vault-password-file=VAULT_PASSWORD_FILES
                        vault password file
  -v, --verbose         verbose mode (-vvv for more, -vvvv to enable
                        connection debugging)
  --version             show program's version number, config file location,
                        configured module search path, module location,
                        executable location and exit

  Privilege Escalation Options:
    control how and which user you become as on target hosts

    -b, --become        run operations with become (does not imply password
                        prompting)
    --become-method=BECOME_METHOD
                        privilege escalation method to use (default=sudo), use
                        `ansible-doc -t become -l` to list valid choices.
    --become-user=BECOME_USER
                        run operations as this user (default=root)
    -K, --ask-become-pass
                        ask for privilege escalation password

  Connection Options:
    control as whom and how to connect to hosts

    -k, --ask-pass      ask for connection password
    --private-key=PRIVATE_KEY_FILE, --key-file=PRIVATE_KEY_FILE
                        use this file to authenticate the connection
    -u REMOTE_USER, --user=REMOTE_USER
                        connect as this user (default=None)
    -c CONNECTION, --connection=CONNECTION
                        connection type to use (default=smart)
    -T TIMEOUT, --timeout=TIMEOUT
                        override the connection timeout in seconds
                        (default=10)
    --ssh-common-args=SSH_COMMON_ARGS
                        specify common arguments to pass to sftp/scp/ssh (e.g.
                        ProxyCommand)
    --sftp-extra-args=SFTP_EXTRA_ARGS
                        specify extra arguments to pass to sftp only (e.g. -f,
                        -l)
    --scp-extra-args=SCP_EXTRA_ARGS
                        specify extra arguments to pass to scp only (e.g. -l)
    --ssh-extra-args=SSH_EXTRA_ARGS
                        specify extra arguments to pass to ssh only (e.g. -R)

```
