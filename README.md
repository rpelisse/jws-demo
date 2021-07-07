# Ansible JWS demo

This playbook demonstrate how to install and upgrade Apache Tomcat (or JBoss Web Server) and also deploy and update a webapp using Ansible.

## Requirements

This demo has been tested on a RHEL 8.4 system using Ansible 2.9.22 (as provided by Red Hat) running wit Python3.

### Red Hat RPM repository to enable

The system needs registered into RHN, with subscription for both Ansible and JWS attached. The following repos having enabled:

    ansible-2.9-for-rhel-8-x86_64-rpms

If you want to install JWS using the RPMs provided by Red Hat, you'll also need to enable the associate repository:

    jws-5-for-rhel-8-x86_64-rpms

The provided role for JWS as also a dependency that needs to be install after Ansible has been successfully installed:

    $ ansible-galaxy install middleware_automation.jws

## Run the demo

Add your RHN creds into a YAML file:

    rhn_username: xxxx@redhat.com
    rhn_password: 'PASSWORD!'

Then run Ansible to install JWS and the demo app:

    $ ansible-playbook -e @rhn_creds.yml -e @version_1.0.yml playbook.yml

To update the application, run again Ansible:

    $ ansible-playbook -e @rhn_creds.yml -e @version_1.1.yml  playbook.yml

Note: if you have register the system into RHN, attached the appropriate subscribtion and enable the repo associated to JWS, you can edit the defaults values of the jws role to install the software directly with RPM, without providing your RHN credentials to Ansible:

    ---
    jws:
    #  package: jws5
    # uncommend 'package:' and comment the next line
      rhn_url: 'https://access.redhat.com/jbossnetwork/restricted/softwareDownload.html?softwareId=90361'
      catalina:
        home: /var/opt/rh/scls/jws5


