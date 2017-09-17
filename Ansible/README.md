# Development image

This directory contains ansible scripts which deploy all the applications needed to do basic unix/java development.

This scripts will install the following applications:
- ActiveMQ
- Ansible
- Ansible-lint
- Apache2
- Atom
- Eclipse
- Git
- Gitkraken
- Google Chrome
- IntellIJ
- Maven
- PHP
- Postgresql
- SoapUI
- Tomcat
- VisualStudioCode

To run these scripts, execute the following command:

```ansible-playbook -i inventory development.yml```