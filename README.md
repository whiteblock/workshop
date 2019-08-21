# Getting started

## Dependencies
We use the virtualbox provider with vagrant.
You can find the documentation for installing vagrant [here](https://www.vagrantup.com/docs/installation/).
The instructions for virtualbox are [here](https://www.virtualbox.org/wiki/Downloads)
If you are on debian, you can also use the command `sudo apt install -y virtualbox`

## Starting Genesis OSS
After installing the dependencies, you are pretty much done.
All you need to do is clone this repo, and then run `vagrant up`. This will spawn up the genesis environment inside of a virtual machine

## Go inside the vm
You can get inside the vm by using the command `vagrant ssh`

## Note
If nonce is not found on your box, you can fetch it using `wget https://storage.googleapis.com/genesis-public/nonce/master/bin/linux/amd64/nonce`
## Building a simple testnet
Inside the box, you will be using the nonce tool. To build your a simple testnet, you can use the command `nonce build -b geth -i light -n 2` 

## Applying simple network constraints.
You can use the command `nonce netconfig all` to apply network constraints between the nodes. Try out `nonce netconfig all -d 10` and you will notice that the RTT between the nodes is 10ms.