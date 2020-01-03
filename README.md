# website

DevOps project from http://hedge-ops.com/devops-project/

Phase 1: Simple Website
Create an account on https://github.com/
Create a repository named website on GitHub
Clone your website repository locally using your terminal (Terminal on a mac or PowerShell on windows).
Create a branch called feature_index
Add an index.html to the branch that says Hello, World! in the text. You’ll want to make the change with Visual Studio Code
Check that in
Create a pull request for your branch to be merged into master and assign the pull request to your mentor. If you don’t have a mentor, assign it to me, mhedgpeth! :)
Merge your pull request into master after it’s approved
What We’re Learning
In order to work well with DevOps automation and tooling, you need to know the basics about source control and editing code. This gives you that foundation. It also gives us something to deploy in future phases.

Resources for Phase 1
Try Git in 15 minutes
Getting Started with Visual Studio Code
Codecademy Learn HTML
Phase 2: Simple Webserver
Now that you have a website, you want to now create a webserver. This is a machine that will provide other machines the contents of your index.html file from phase 1. This machine will be a linux machine hosted on Microsoft Azure Cloud with nginx running on it.

Create an account on Azure and activate your free trial
Create an ubuntu virtual machine on Azure
SSH to that machine. If you’re on windows use Matt Wrock’s guide to getting a ssh client.
Set up nginx on the machine
Clone your git repository to /var/www/html on the server
Using the public ip assigned to your ubuntu server, access the website (i.e. http://[your-ip]). Your website should show up.
Have a friend on another computer do this. They should see the website too. Magical!
What We’re Learning
My friend Nathan Harvey has said to me that you can’t automate that which you do not understand. If you’re going to “do the DevOps” but can’t do it manually, then you’re going too fast! So we’re learning the basics here of setting up a machine.

Resources for Phase 2
Setting Up Linux Virtual Machine on Azure
Nginx Tutorial
Nano Tutorial for editing text files in an ssh session
Phase 3: Deploy a Change
Now it’s time to deploy a change! Let’s do this the old fashioned way the first time around.

Create a new branch on your repository named feature_myname.
Update index.html to say “Hello, Michael!”
Create a pull request, get it reviewed, and merge it
On your webserver, update your index.html file from GitHub.
Get on twitter and send me a message @michaelhedgpeth with a link. Show me that I didn’t waste my time! :)
What We’re Learning
This is how a majority of people have deployed things for a long time. The manual way. You can’t realize what problems different tools solve before you do it manually. I’m purposely not giving you the exact steps to follow because I want you to find those steps on your own or with a mentor. Google it! This is how you learn.

Phase 4: Create a Chef Cookbook to Automate Machine Setup
Now think about what your life would be like if you had to do the above steps thousands of times on hundreds of servers. Your life would not be fun, and in addition to that you would have hundreds of servers that were all a little bit different because, over time, you weren’t consistent. This is why you use something like Chef.

This is a big technical jump from the previous phases. Take your time here. If you’ve never done this stuff you might spend a couple of weeks on it. You’ll have questions. Get on the Chef Community Slack and post them on the #general channel. Don’t be afraid; we all were here and support you!

On GitHub create a repository called my_website.
Clone that repository locally and switch to a branch called feature_nginx
Set up nginx using the package resource
Use Test Kitchen to make sure your cookbook installs the package. Use kitchen with a Policyfile. There will be a Policyfile.rb in the cookbook that defines your run list if you’re doing this right.
Write an Inspec Test that ensures the package is installed
Create a PR and get it merged
Create another branch called feature_website
Using the git resource clone your repository on GitHub
Write another inspec test to make sure that the website is served when you go to http://localhost and that the contents contain “Hello, Michael!”
Make sure that kitchen test works
Create a Pull Request and Merge into master
Resources for Phase 4
Learn Chef Rally. If you’re new to Chef, spend a lot of time here. Like days. Get through the basics and what I write above will make a lot more sense
My Policyfiles Post. My description of that feature. Do yourself a favor and use it. It will simplify your life.
Annie’s InSpec Tutorials. Still the best place on the internet to learn InSpec.
Phase 5: Deploy Your Chef Cookbook to Azure
Now it’s time to use your Chef Cookbook as a way to not have to manually deploy and update your machine. After you do this step, you’ll be able to consistently create as many machines as you want, with very little effort!

Create a new virtual machine on Azure using the portal
Create an account and organization on manage.chef.io. If you did the learn chef rally above, you should already have this set up.
Push your cookbook policy to the chef server (see my blog post for the exact command.
Bootstrap your node with the chef server. This will run the policy on that node, setting up nginx and everything!
Hit the public IP associated with the node and see that it serves your website perfectly! Magic!
Now deploy a new change to your website and call it “Hello, Automated World!”. Tell me about it (@michaelhedgpeth on twitter). I’ll give you a high five for getting this far!
What We’re Learning
Hopefully you see the benefits of automating the setup of the machine. From now on, everything is consistent and just works. Your drama for making changes goes down. And you can do this as many times as it’s called for!

Phase 6: Automate Creation of VMs in Azure with Terraform
Now that we have a Virtual Machine that we can easily set up, you might be tempted to quit. But there’s something lingering there: even though you automated what was inside of the virtual machine, you still have to manually set up the machine itself. This is easy enough when you have one machine, but what if you have hundreds? That’s where Terraform comes in:

Create a new repository in GitHub called website_provision
In that repo, create a terraform script that creates a virtual machine within a network with an external ip address
Make your terraform script bootstrap the VM with your Chef Server and assign it to your policy
Wath with awe how terraform allows you to create and destroy your entire stack, all the way from the machines itself to what’s on the machines (with Chef).
What We’re Learning
The environment within which your application runs is one of the most complicated aspecs of the application. Thus, you should invest in automating that and keeping yourself away from the user interface. Terraform is a great tool for this.

Phase 6 Resources
Terraform Resources
Azure Terraform Provider
Azure Terraform Examples
Phase 7: Workflow Automation with Jenkins
Now that we have an automated process that will deploy our stuff, we want to make our workflow easy to execute with Jenkins. Before you move on I highly recommend Wes Higbee’s Jenkins class on Pluralsight. It’s well worth the trouble. That will give you the context you need to go through these steps:

Create a rakefile for your my_website cookbook using [my blog post])(http://hedge-ops.com/cookbook-development-with-rakefile/) as a guide.
Create a Jenkinsfile for your cookbook using my blog post as a guide
Create a Jenkins server. If you took the class you may already have one.
Create a Jenkins build for my_website that runs on all branches (using the multi-branch pipeline, as Wes explains in the course)
Create a branch called broken and add code that will break your cookbook
Check it into the branch, and watch Jenkins tell you it’s broken!
What We’re Learning
We’re automatically providing the accountability people need to know that their software still works. It’s better to learn that as you’re making the changes rather than when they get to production. So Jenkins helps us see how, when we change software over time, that software still meets our expectations. It reinforces the best practices for your team: you should run test kitchen before checking in changes. The safety imposed by Jenkins will keep you on the straight and narrow path!

Resources for Learning
Getting Started with Jenkins 2
Extra Credit
I think if you do the above project, you’ll be well on your way to getting things working. Here are some other ideas, for extra credit:

With Hashicorp Vault store a secret and have your chef cookbook (using the vault gem) read the secret and write it to your web page
Create a Jenkins pipeline that will deploy your terraform templates
Instead of using Chef, use Docker (perhaps with Habitat) to deploy your application
