# Conductor

   Project: Bootstrapping a Debian/Ansible conductor host
   
# Initial host setup

```
   Input: Debian 9.6 Stretch DVD
   
   Decisions to be made in advance : airgapped or online install, free only or including non-free firmware as well.
   
   Sources :
       https://cdimage.debian.org/debian-cd/current-live/amd64/iso-hybrid/debian-live-9.6.0-amd64-xfce.iso
       https://cdimage.debian.org/images/unofficial/non-free/images-including-firmware/current-live/amd64/iso-hybrid/debian-live-9.6.0-amd64-xfce+nonfree.iso
       
     In case of an airgapped or offline install, also download the most recent applicable (check https://packages.debian.org/search?keywords=debootstrap&searchon=names&exact=1&suite=all&section=all) version off debootstrap. At this moment this is http://ftp.debian.org/debian/pool/main/d/debootstrap/debootstrap_1.0.89_all.deb
               
   Output: live environment in a separate hierarchy or a live system, containing the initial empty conductor host
   
   Known values afterwards:
       domain name                 : 
       hostname                    :
       ip address/subnetmask       :
       gateway                     :
       name servers                :
       root password crypt         :
       initial username            :
       initial user password crypt :
```

# Default directory layout

[From Ansible Best Practices](http://docs.ansible.com/ansible/latest/playbooks_best_practices.html#directory-layout)

```text
production                # inventory file for production servers
staging                   # inventory file for staging environment

group_vars/
   group1                 # here we assign variables to particular groups
   group2                 # ""
host_vars/
   hostname1              # if systems need specific variables, put them here
   hostname2              # ""

library/                  # if any custom modules, put them here (optional)
module_utils/             # if any custom module_utils to support modules, put them here (optional)
filter_plugins/           # if any custom filter plugins, put them here (optional)

site.yml                  # master playbook
webservers.yml            # playbook for webserver tier
dbservers.yml             # playbook for dbserver tier

roles/
    common/               # this hierarchy represents a "role"
        tasks/            #
            main.yml      #  <-- tasks file can include smaller files if warranted
        handlers/         #
            main.yml      #  <-- handlers file
        templates/        #  <-- files for use with the template resource
            ntp.conf.j2   #  <------- templates end in .j2
        files/            #
            bar.txt       #  <-- files for use with the copy resource
            foo.sh        #  <-- script files for use with the script resource
        vars/             #
            main.yml      #  <-- variables associated with this role
        defaults/         #
            main.yml      #  <-- default lower priority variables for this role
        meta/             #
            main.yml      #  <-- role dependencies
        library/          # roles can also include custom modules
        module_utils/     # roles can also include custom module_utils
        lookup_plugins/   # or other types of plugins, like lookup in this case

    webtier/              # same kind of structure as "common" was above, done for the webtier role
    monitoring/           # ""
    fooapp/               # ""
```


