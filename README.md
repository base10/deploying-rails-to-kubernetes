# RailsConf 2021 Workshop: Deploying Your Rails Application to Kubernetes

## Welcome!

This workshop is scheduled for April 12, 2021 from 1 PM to 3 PM EDT. We are super excited to share this workshop with you.

## The workshop

Kubernetes has a lot of DevOps mindshare and is how shops like GitHub and Shopify are deploying their apps. But, what is Kubernetes? What does it mean for deploying your application? Do you need it?

In this workshop, we'll answer by migrating a small Rails application to Kubernetes. We'll build up the deployment tooling necessary to stand the application up on a small Kubernetes cluster.

We'll also explore the core concepts and considerations of adding Kubernetes to your deployment pipeline, including Kubernetes operations, preparing for ephemeral infrastructure, data storage, and more.

### Structure

We're slated for two hours of workshop. We'll take a couple of short breaks during those two hours.

Nathan and Alex will be around on Discord after the workshop to answer questions and give further help.

## Prerequisites

- A computer capable of running Ruby on Rails and two VirtualBox virtual machines
    - We recommend a recent laptop with at least two physical CPU cores and at least 8 GB of memory
        - Plan on ~3GB of memory being used by the VMs
    - You will need up to 20 GB of disk space to run two Ubuntu virtual machines and a small Rails app
        - It probably will not be that much, but as I write this, I'm using close to 7 GB between the two machines
    - The smoothest path will be via macOS, since that's where our direct experience is
    - Windows and Linux users should also be able to successfully set-up and run the Rails app locally and
- Basic experience with Rails applications
    - Rails beginners are _welcome_,

## Setup

You will want to have set-up completed before attending the workshop. We will review the prerequisites and what we're doing during the workshop, but, we are not setting aside time to install software or create accounts during the workshop.

### Exceptions to suggested installations

"Nathan, Alex, there are other valid ways to install this software that's less resource intensive!"

Granted! We're prioritizing on "easiest path to get up and running". If you want to experiment with other virtualization libraries, use smaller VM images, whatever, _you can_, however, you will be on your own.

### Software

- [Homebrew](https://brew.sh)
    - For macOS users, you might already be using this tool, and for the next steps, you may find it helpful to use `brew install X` as your installation method
- Ruby 2.7.2
    - Install via `rbenv`, `rvm`, `chruby` or other tool
- Bundler 2.2
    - `gem install bundler` on the command-line
- [VirtualBox](https://www.virtualbox.org)
    - For macOS users, you can install via Homebrew
        - `brew install virtualbox`
    - Linux, Windows, and Mac users can [download VirtualBox directly](https://www.virtualbox.org/wiki/Downloads)
        - Click on the link
        - Select your operating system
        - Install according to the downloaded package instructions
- [Vagrant](https://www.vagrantup.com)
    - macOS users can install via Homebrew
        - `brew install vagrant`
    - Linux, Windows, and macOS users can [download Vagrant directly](https://www.vagrantup.com/downloads)
        - Click on the link
        - Select the appropriate OS
        - Click "Download"
        - Install according to the downloaded package instructions

### Repository

The workshop is using [Link](https://github.com/base10/link), a tiny and simple Rails application. Please clone that repository and follow Link's set-up instructions to get a local instance of the application running.

### Initialization

- After installing the Software above, clone this repository locally
- Within your local clone of this repository, change directories in `vagrant`
- `vagrant up`

At this point, you will download a Vagrant box for Ubuntu 20.04, which will be used to create two virtual machines. Provisioning will take a few minutes.

#### Rerunning provisioning

If provisioning is interrupted or there's a need to update the existing images to take new provisioning instructions into account, from the `vagrant` directory, you can run `vagrant provision`

#### Connecting to the machines

You will have two VMs

- `workshop-microk8s.local`
- `workshop-datastores.local`

Connect to them like so:

- `vagrant ssh workshop_microk8s`
- `vagrant ssh workshop_datastores`

#### Cleaning up after the workshop

If you want to stop the VMs, but keep them around:

`vagrant halt`

When you're finished with the VMs entirely, you can clean them up. NB: This is destructive!

`vagrant destroy`

### Installation Help!

If you need extra help getting everything installed and running, Alex and/or Nathan are hosting Discord office hours ahead of the workshop:

- Friday, April 9: 2 to 5 PM EDT
- Monday, April 12: 9:30 to 11:00 AM EDT

### Service account set-up

**Forthcoming**

- Heroku to get the initial state of the app up-and-running
    - Not strictly necessary, but we'll cover it lightly in the first section of the workshop
- Transactional email

## Workshop

The workshop runs from 1 pm to 3 pm EDT, April 12. You'll need to be in the RailsConf 2021 Discord server to participate.

There will be a short break during the workshop.

## Resources

- [Vagrant Docs](https://learn.hashicorp.com/vagrant)
- [Vagrant Boxes](https://app.vagrantup.com/boxes/search)
- [Ubuntu Focal64 box](https://app.vagrantup.com/ubuntu/boxes/focal64)
- [GitHup repo on setting up microk8s](https://github.com/halvards/vagrant-microk8s)
- [CloudHero on setting up dev environments with Vagrant and k8s](https://cloudhero.io/development-environment-with-vagrant-and-microk8s)
- [Using Vagrant with MicroK8S to experiment with Kubernetes](https://gist.github.com/JonTheNiceGuy/66f44e352352c24307bb5ca78c984793)
- [Canonical: Introduction to MicroK8s](https://microk8s.io/docs)

## Credits

**Forthcoming**
