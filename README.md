# Website - Simple DevOps Project

DevOps project from page: [hedge-ops](http://hedge-ops.com/devops-project/).

## Phase 1: Simple Website
1. Create an account on https://github.com/
2. Create a repository named ```website``` on Github
3. Clone your ```website``` repository locally using your terminal (Terminal on a mac or PowerShell on windows)
4. Create a branch called ```feature_index```
5. Add an ```index.html``` to the branch that says ```Hello, World!``` in the text. You’ll want to make the change with Visual Studio Code
6. Check that in
7. Create a pull request for your branch to be merged into ```master```
8. Merge your pull request into ```master``` after it’s approved

## Phase 2: Simple Webserver
1. Create an account on Azure and activate free trial
2. Create an ubuntu virtual machine on Azure
3. SSH to that machine
4. Set up nginx on the machine
5. Clone your git repository to ```/var/www/html``` on the server
6. Using the public ip assigned to your ubuntu server, access the website

*Resources*
* [Setting Up Linux VM on Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-portal)
* [Nginx Tutorial](http://www.gigasacs.net/language/en/2016/05/11/installing-nginx-on-an-azure-linux-ubuntu-16-04-vm/)
