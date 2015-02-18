# hostr
Dynamic hostname interpolation and supplement to /etc/hosts

You have a bunch of machines in the cloud. They come and go so often (livestock, not pets) so you don't bother putting their IPs in /etc/hosts. If only there was a way for your dev machine to automatically know the address to your VMs in the cloud, and connect to them quickly without you needing the IP address. Oh no way, this project does just that? Killer sick, dude.

## Example usage

    $ ssh core@$(hostr my-vps)

    $ ssh user@$(hostr my-vps2)
    
or
    
    $ ssh core@`hostr my-vps3`
    
hostr uses the power of bash* command substitution. You can use hostr anywhere that uses bash*:

    $ echo "my vps named mega-vps is pretty cool and it's IP address is $(hostr mega-vps)"


## Installation

hostr is written in javascript, so node.js is a dependency. Get node here: http://nodejs.org/download/

Once you have node installed, clone hostr from github onto your computer. I like putting it in a directory, ~/scripts.

    $ mkdir ~/scripts
    $ cd ~/scripts
    $ git clone https://github.com/insanity54/hostr
    $ cd hostr
  
Now we need to satisfy some of hostr's javascript dependencies

    $ npm install
    
K, now we need to give hostr some information sources. These sources are your VPS/VM hosting services. hostr queries these sources using their api, and finds the IP address of the host you specify using it's human readable lable. Right now, vultr is the only suported source. We tell hostr about our vultr account by editing the hostr config file, `~/scripts/hostr/config.json`

    {
        "VULTR_API_KEY": "enter your vultr api key here"
    }h
  
Gr8, now we need to make the hostr command available to bash*. We do this by adding an alias to the end of our ~/.bash_aliases file. For other shell aliases, check their docs. Our ~/.bash_aliases file needs this line:

    alias hostr='~/scripts/hostr/hostr.js'
    
But we can automate adding that with the following command:

    $ echo -e "\nalias hostr='~/scripts/hostr/hostr.js'" >> ~/.bash_aliases
  
That's it! hostr is ready to use. Try it out!

    $ echo "$(hostr my-vps-name)"


   
    
    


## Foot notes

* also sh, ksh, and whatever the cool kids use these days
