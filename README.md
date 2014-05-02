Take the contents of config and add it to your .ssh/config
```
# To connect to Daniel Glauser's VM
Host daniel
User vagrant
ProxyCommand ssh -q theden nc -q0 localhost 8675

# To connect to Sean Duckett's VM
Host seanduckett
User pair
ProxyCommand ssh -q theden nc -q0 localhost 3742

# Misc
Host theden
Hostname denofclojure.org
ForwardAgent yes
```
Once we arrange for a meeting time I execute the following alias:
```
alias tunnel-dnc="ssh -nNT -R 8675:localhost:22 daniel@denofclojure.org"
```

(NOTE: this would vary as to whom is tunneling for the setup. Sean would set the port to 3742, Daniel to 8675....)


then in another shell I run the alias:
```
alias tmux-dnc="tmux -2 -S /tmp/denofclojure attach || tmux -2 -S /tmp/denofclojure new-session 'chmod 777 /tmp/denofclojure && ${SHELL}'"
```

I add your key to my .ssh/authorized_keys file.

Then once you are on my box you execute the tmux-dnc alias and voila, we're connected!
I know it seems like a lot but it's pretty easy once it is setup. The usual case is you say, "Hey Daniel let's pair." I say, "Okay, come on over, my tunnel is up." You ssh daniel, then type tmux-dnc once you are in and we're pairing.

# Virtual Machines for pairing

I'm using Vagrant to manage VirtualBox VMs.

1) Ubuntu 12-10, 64 bit image:

You would say:

  vagrant init ubuntu12-10 http://cloud-images.ubuntu.com/quantal/current/quantal-server-cloudimg-vagrant-amd64-disk1.box

2) Follow the Vagrant instructions, add the box, and you should be able
to bring it up without issue.

3) If you can bring the box up just fine, then edit the local config to
forward any ports you need. If we're remote pairing you would want to
forward the port specified earlier. The Vagrant docs include the info:
