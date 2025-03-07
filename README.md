
# Homelab-ansible

Creating a proper ansible directory hopefully to follow industry standards
based off of  
https://docs.ansible.com/ansible/latest/tips_tricks/sample_setup.html  

# Command examples  

To run all tasks labeled update against objects with the "common" role:  

    ansible-playbook -i production site.yml --tags update  

# File Structure

    production                # inventory file for production servers  
    staging                   # inventory file for staging environment  
  
    group_vars/  
        group1.yml             # here we assign variables to particular groups  
        group2.yml  
    host_vars/  
        hostname1.yml          # here we assign variables to particular systems  
        hostname2.yml  
  
    library/                  # if any custom modules, put them here (optional)  
    module_utils/             # if any custom module_utils to support modules, put them here (optional)  
    filter_plugins/           # if any custom filter plugins, put them here (optional)  
  
    site.yml                  # main playbook  
    webservers.yml            # playbook for webserver tier  
    dbservers.yml             # playbook for dbserver tier  
    tasks/                    # task files included from playbooks  
      webservers-extra.yml  # <-- avoids confusing playbook with task files  
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
              main.yml      #  <-- role dependencies and optional Galaxy info  
          library/          # roles can also include custom modules  
          module_utils/     # roles can also include custom module_utils  
          lookup_plugins/   # or other types of plugins, like lookup in this case  
  
    webtier/              # same kind of structure as "common" was above, done for the webtier role  
    monitoring/           # ""  
    fooapp/               # ""  
