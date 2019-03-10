# ansible-test
<b>Nizam Ansible Playbook</b>

Run: ansible-playbook site.yml

<b>Assumptions:</b>
1. Timezone is UTC 0:00 for the servers.
2. User johndoe is an SSH user for the instance, thus only the public key is uploaded to the server
3. Firewall set in AWS Security Groups to allow SSH from within private VPC and port 80 from public.
4. Only Wordpress installation is done in the playbook; no setting up of Wordpress to the database.
   When visiting the site by IP, it will show the Wordpress setup config page.


<b>Notes:</b>
1. Hosts file is updated in /etc/ansible/hosts file and must contain the below section.<br>
   [servers]<br>
   host1 ansible_ssh_host=X.X.X.X

2. Playbook tested in Amazon Linux 2 instance (based on CentOS 7).
3. There will be a few warnings as some of the tasks use 'tar' and 'curl'.
4. An earlier version of php-fpm was installed due to errors detected (for the later versions) when deploying the playbook.<br>
   When php 7.1 was installed, there were several missing packages from the rpm file.<br>
   When php 7.2 was installed, playbook was deployed successfully; however, website was inaccessible.
5. Passwords that need to be changed:<br>
   roles/percona-mysql/defaults/main.yml > mysql_root_password<br>
   roles/wordpress/vars/main.yml > wp_db_password<br>

<b>Playbook Roles</b>
1. users<br>
Create user for host<br>

2. common<br>
Update and installation of packages<br>

3. ntp<br>
Setup and configuration of NTP<br>

4. nginx<br>
Installation and configuration of Nginx web service<br>

5. php-fpm<br>
Installation and configuration of php-fpm<br>

6. percona-mysql<br>
Installation and configuration of Percona MySQL<br>

7. wordpress<br>
Installation of Wordpress<br>

8. logtime<br>
Setup and configuration of logtime service<br>
