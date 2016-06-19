# **Ansible Created Apache Storm Cluster**

by Joaquin Menchaca on May 2nd, 2016

These are [Ansible](http://ansible.com/) provisioning scripts that create an [Apache Storm](http://storm.apache.org/) cluster.

Using Vagrant as proof of concepts.  Any set of systems, provided an inventory, should work for these scripts.

# **Requirements**

### **Software Requirements**

Whatever system you use to run provisioning (controller workstation), it must be able to run and use Ansible (and Python).  These typically rules out Windows, but you are welcome to try with something like [CygWin](https://www.cygwin.com/) or [MSYS2](https://msys2.github.io/).

To run the demonstration system provided to try out these scripts, you'll need [Vagrant](https://www.vagrantup.com/) with [Virtualbox](https://www.virtualbox.org/wiki/Downloads).  

#### **Mac OS X**

A convenience script has been provided for Apple OS X (now called Mac OS, not to be confused with Mac OS 9): `install_osx.sh`.  This requires XCode Command Line Tools and [Homebrew](http://brew.sh/) to be installed.

### **Configuration Requirements**

These scripts are tested with a [Vagrant](https://www.vagrantup.com/) environment working on [Virtualbox](https://www.virtualbox.org/wiki/Downloads).  They should work on any environment provided these requirements are met:

* Appropriately Name Systems - matching the patterns below
  * `*Zookeeper*`
  * `*Supervisor*` - one or more supervisors
  * `*Nimbus*`
* [Ansible](http://ansible.com/) SSH Requirements
  * able to log into systems without a password
  * able to sudo without a password
  * direct root access through SSH is naughty (not supported, don't even try)
  * appropriately crafted inventory or dyanmic inventory
    * dynamic vagrant inventory one is provided (`config/inventory.py`)
    * reconfigure `ansible.cfg` to use the correct inventory, or override with `-i` switch
    * `common` role can be commented out (this is for SSH/DNS convenience in Vagrant environment)
