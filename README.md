# vm-drupal-elk

Vagrant project for Drupal and the ELK stack
============================================
You will get two vagrant managed VMs out this repository.  One running Drupal
and the other running the ELK (Elasticsearch, Logstash, Kibana) stack.  Things
have been setup so that Drupal's logs are stored in Elasticsearch.  These can be
explored using Kibana which provides a web interface for the logs.

Purpose
-------
There are quite a few online tutorials and presentations on how to save and use
Drupal's logs in Elasticsearch.  But I have not found any online demo.  This
Vagrant project tries to fill in that gap.  It is not an online demo of course,
instead it will let you spin two VMs running Drupal and the ELK stack.  You can
then find out how it feels like to play with Drupal's logs from inside Kibana's
web interface.  If you like it, you can then use the relevant configuration
files to setup your own environment.  If you *do not* like it, you can destroy
the VMs and move on without losing much time :)

How to run
----------
  1. Install Vagrant if necessary.  This project has been developed using version 1.8.1.
  2. [Install Ansible] (http://docs.ansible.com/ansible/intro_installation.html).  The playbooks have been tested in version 2.1.0.0.
  3. Issue "vagrant up" from the project directory.  It can take **up to an hour** for both VMs to be ready and running for the first time.  Total memory requirement is **nearly 2GB**.
  4. The hostnames of the VMs are *drupal.dev* (192.168.33.33) and *elk.dev* (192.168.33.35).  You may have to add these to your operating system's hosts file before accessing them from a web browser.
  5. Once the VMs are up, login and logout of [Drupal] (http://drupal.dev/) as admin/admin.  This should generate at least one log entry.  The Drupal instance is using the "minimal" profile which makes it look quite bland.  Let that not surprise you.
  6. Open Kibana from http://elk.dev:5601/.  On the first visit, you will find yourself in Kibana's [index setup screen] (https://www.elastic.co/guide/en/kibana/current/tutorial-define-index.html).  Once past this, [import] (https://www.elastic.co/guide/en/kibana/current/managing-saved-objects.html) the "Drupal" search filter from the "Settings > Objects > Import" tab.  You will find the search filter file that needs importing as part of this repository at "the-ansible-files/conf/elk/kibana-drupal-search-export.json". Afterwards, the "Discovery" tab will let you [play] (https://www.elastic.co/guide/en/kibana/current/discover.html#load-search) with Drupal's logs.

Software versions in the VMs
----------------------------
  * Operating system: Debian 8 (Jessie) for x86
  * Drupal: 8.x
  * Elasticsearch: 2.3
  * Logstash: 2.3
  * Kibana: 4.5
  * Curator: 4.x

Notes on Ansible playbooks
--------------------------
The playbooks in this repository are very basic and are not at all
production-grade.  You can use them as a basis for writing your own playbooks.
The nature of the playbook syntax means anyone can read them and figure
out what is going on.  That understanding along with the configuration
files are the primary take-away from this repository.
