# Programming Cookbook

## Fun

Source: https://www.digitalocean.com/community/tutorials/top-10-linux-easter-eggs

### ASCII Art Star Wars Through Telnet

```
sudo apt-get install telnet
```

```
telnet telehack.com
```

or

```
telnet towel.blinkenlights.nl
```

### Star Wars Traceroute

A newer tribute to Star Wars has been achieved by Ryan Werber by naming the network hops to a specific address.
If you run traceroute, a program that traces the path of packets to a remote host, you will see the intro to Star Wars in the network names along the way.

```
traceroute -m 254 -q1 obiwan.scrye.net
```

### Vim and Douglas Adams

Open the editor from the command line:

```
vim
```

Type the following to access a special vim help menu:

```
:help 42
```

### Emacs Games

```
sudo apt-get install emacs
```

You can find out what games are available by checking out this directory:

```
cd /usr/share/emacs/*/lisp/play
ls
```

To execute them, open Emacs:

```
emacs
```

Next, type the `Esc` key, followed by `x` (for execute), and then type the name of the game you wish to start:

```
Ecc-x
pong
```

To quit Emacs when you are finished, type `Ctrl`, followed by `x`, and then `Ctrl` and `c`:

```
Ctrl-x
Ctrl-c
```

### Steam Locomotive

Source: https://www.linuxshelltips.com/sl-run-locomotive-train-in-terminal/

```
sudo apt install sl
```

Run the command to verify the installation. If installed and working correctly, you should see the train animation shown below.

```
sl
```

#### Basic Usage of SL (Steam Locomotive) in Linux

If you call the command with a parameter `-a`, it will show the train animation, with people on the train shouting for help.

```
sl -a
```

Parameter `-l` shows a smaller train in the animation.

```
sl -l
```

Similarly, with '-F' parameter, the train will appear as if it is flying, instead of going in a straight line.

```
sl -F
```

There is another parameter '-e' which will allow the user to close the animation with a Ctrl + C signal when used.

```
sl -e
```

### Apt-get Cows

On Ubuntu and Debian, the apt-get package manager has had an embedded easter egg for a long time now.

```
apt-get help
```

The last line tells us that the easter egg is active in this version of apt. Type:

```
apt-get moo
```

### Aptitude Cows

With apt-get’s affinity for cows, users may be curious as to whether aptitude, another apt tool, also implements a fun easter egg.

```
aptitude moo
aptitude -v moo
aptitude -vv moo
aptitude -vvv moo
aptitude -vvvv moo
aptitude -vvvvv moo
aptitude -vvvvvv moo
```

### Fun with Cowsay and Fortune

If you need some more cheap amusement at the command line, and didn’t get your fill of cows from the “apt” easter egg, you can download `cowsay` and `fortune`.

```
sudo apt-get install fortune cowsay
```

Cowsay inserts any input into a word bubble and draws an ASCII cow to talk to you:

```
cowsay "hello, I'm a cow"
```

The fortune program spits out quotations, fortunes, jokes, nonsense that can be piped into cowsay:

```
fortune | cowsay
```

If you’re not too fond of cows, you can get other characters as well:

```
fortune | cowsay -f tux
```

For a full list of the available characters, type:

```
cowsay -l
```

### Insult Users with Sudo

You can configure sudo, used to elevate the privileges of a command, to insult users when they type in an incorrect password.

```
sudo visudo
```

Near the top, add a line that reads:

```
Defaults insults
```

Save and close the file.
Next, empty the cache that stores your password for a certain amount of time and then mistype your password for a sudo command:

```
sudo -k
sudo ls
```

## FTP

Link: https://github.com/kevinnguyen20/programming-cookbook/wiki/FTP

## Search Engine

### What is robots.txt

Source: https://developers.google.com/search/docs/advanced/robots/intro
