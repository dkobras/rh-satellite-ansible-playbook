# This is a playbook to set up a Satellite 6 server

## Author, Copyright and License
This playbook is created by Luc de Louw <luc@delouw.ch>, <ldelouw@redhat.com>. It is free software licensed under the terms of the GNU General Public License GPL v3 or later. A copy of the license can be obtained here: http://www.gnu.org/licenses/gpl-3.0.html

## Motivation
I've wrote this Playbook because I do a lot of experiments with the Red Hat Satellite, trying new stuff and 
sometimes it breaks (i.e. when upgrade to a new beta relase). Manual installation takes a lot of time and it is boring as hell. Work smarter, not harder!

## Scope
This playbook is not meant for daily tasks such as creating and provision new hosts and the like,
it's just for the initial configuration

## Things covered in this playbook
At the moment, the Playbook covers the most important topics for getting a Satellite up and running

## Compatibility
This version of the playbook was tested to be working with Satellite Version 6.8 and 6.9.
For Satellite 6.10 beta, at least currently, in the vars.yml you need to set the operatingsystem to i.e. "RedHat-8.4", while it is "RedHat 8.4" for older Satellites

## Prerequisites
* Subscribe the system, add the required repositories as described in the document https://access.redhat.com/documentation/en-us/red_hat_satellite/6.9/html-single/installing_satellite_server_from_a_connected_network/index
* Install the Satellite,python2-jmespath and the Ansible collection for Red hat Satellite: *yum -y install satellite ansible-collection-redhat-satellite python2-jmespath*
* Satellite Installer was run with the enabledment of the TFTP feature:
*satellite-installer --scenario satellite --foreman-initial-organization=lab --foreman-proxy-tftp=true*
* Clone this repo: *git clone https://github.com/ldelouw/rh-satellite-ansible-playbook.git*

## Things *NOT* set up:
For security reasons (I dont want to accidentially leak some real life credentials)
* Register and subscribe the Satellite to Redhat CDN
* Setting up an IPA Realm
* Setting up a libvirt compute resource, however, an example is provided but commented out

For technical reasons
* Running the Satellite installer (Just takes too long to execute and brings no benefit)
* Anything that has to do with Puppet, as Puppet ist depricated in Satellite 6

For the sake of lazyness
* Using more than one Organisation. If you are using more than one Org, please use
  multiple vars.yml files per Org.

To be done
* More sophisticated activation key configuration such as subs and repo overrides
* Creating a Letsencrypt cerfiicate using certbot
* More general settings
* IPA/Kerberos authentication
* Remove "Default Location"
* Configuring Capsule servers

## How to use
First of all, edit the vars.yml file, replace everything with example.com 
with your real life environment. Please also read the comments for better understanding

Alter that, the passwd.yml vault password needs to be changed with *ansible-vault rekey passwd.yml*, the password is *changeme*. Edit the passwd.yml file with *ansible-vault edit passwd.yml* and use your real Satellite password and if needed uncomment the default_http_proxy_passwd and change to the real world Proxy password

Then, simply run it with *ansible-play sat6.yml --ask-vault*

Note: It's recommended to have some basic Ansible knowledge to operate this playbook.

## Contributions
Contributions are very welcome :-) Just send me a pull-request

