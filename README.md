Add the following to a file called .ssh/config

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

Once we arrange for a meeting time I execute the following alias:
alias tunnel-dnc="ssh -nNT -R 8675:localhost:22 daniel@denofclojure.org"

then in another shell I run the alias:
alias tmux-dnc="tmux -2 -S /tmp/denofclojure attach || tmux -2 -S /tmp/denofclojure new-session 'chmod 777 /tmp/denofclojure && ${SHELL}'"

I add your key to my .ssh/authorized_keys file.

Then once you are on my box you execute the tmux-dnc alias and wallah, we're connected.
I know it seems like a lot but it's pretty easy once it is setup. The usual case is you say, "Hey Daniel let's pair." I say, "Okay, come on over, my tunnel is up." You ssh daniel, then type tmux-dnc once you are in and we're pairing.
