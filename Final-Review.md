# Topic Overview of Final Exam

### also important
* ssh keys
    * private vs public (and where to put which)
      * private keys need to be kept secure.  These are not for public use 
    * ssh-keygen
    * SSH is the standard for remote access to a system
    * Encrypts your password & session data
    * Tunnels other network connections – we could have a system that requires we use X-Server to see the remote application
    * Offers clients for most Operating Systems
    * Can use keys for host authentication
    * $ ssh remote_username@host
      * When you make a connection, it gets added to ~/.ssh/known_hosts
* sftp: secure file transfer protocol
   * File transfer program from remote to local or from one host to another
* compression: allows you to take up less disk space
   * Compression techniques:
      * Lossless: formats that lose no data (or strive to)
         * File can be restored to original
      * Lossy (a big concern for images): data's quality is compromised
         * Original form cannot be recovered
   * using .zip for folders allows you to quickly compress and unpack files
      * time efficient, but not data efficient
   * gzip (GNU zip) 
      * compress with 'gzip filename' 
      * uncompress with 'gunzip filename'
      * Compressing is algorithmically changing the data to make it smaller.
   * tar
      * tar cvf archive.tar files directories
         * C is for create, v is for verbose, f tells it the first argument will be the filename of the tar archive to create
      * tar xvf archive.tar - where x is for extract
      * tar tvf archive.tar - where t is for table of contents
      * we can compress a tar archive with gzip to compress again
      * tar bundles, but doesn't compress
      * It keeps info about file permissions, and it has the file contents in plain text
* checksums
   * Definition: A checksum is a sequence of numbers and letters used to check data for errors. If you know the checksum of an original file, you can use a checksum utility to confirm your copy is identical.
   * Algortithms used include:
      * MD5 (128-bit)
      * SHA-1 (160-bit)
      * SHA-256 (256-bit)
      * SHA-512 (512-bit)
   * MD5 & SHA-1 are good for checking corruption / transfer integrity, but not a guarantee
   * SHA-256 is best practice right now
   * Finding Checksums:
      * Windows:
         * Get-FileHash file_name –Algorithm MD5 / SHA1 / SHA256
      * Linux:
         * md5sum
         * sha1sum
         * sha256sum 

      




### bash
* bash scripting
    * if statements:  
        if [CONDITION_usually_from_`test`]; then  
            stuff  
        elif [Other_conditions]; then  
            stuff  
        else  
            stuff  
        fi
        
        * example in powerpoint:
        if [ -r somefile ]; then
            content=$(cat somefile)
        elif [ -f somefile ]; then
            echo "The file 'somefile' exists but is not readable to the script."
        else
            echo "The file 'somefile' does not exist."
         fi
    https://www.geeksforgeeks.org/conditional-statements-shell-script/
        
    * loops
        * for loops:  
        for i in LIST  
        do  
            stuff with $i  
        done
        
        * example in powerpoint:
        for i in 1 2 3 4 5
        do
            echo "Welcome $i times"
        done
        (can’t use $i until i is initialized)
        https://www.cyberciti.biz/faq/bash-for-loop/
        
        * while loops:  
        while [CONDITION]  
        do  
            stuff  
        done
         
        * example in powerpoint:
        x=1
        while [ $x -le 5 ]
        do
            echo "Welcome $x times"
            x=$(( $x + 1 ))
        done
        https://www.cyberciti.biz/faq/bash-while-loop/

    * using `test` flags
        * conditionals in scripting
        * remember you don't need the word `test`, you can just use the the conditional provided by `test`
    * arguments and how to access arguments in scripts
        * to access individual arguments: $# where # is the argument from the command line
        * to access all arguments: $@
        
* regular expressions
   * https://regex101.com/
   * Week 8 slides 15-18
   * https://regexone.com/problem/matching_filenames
   * https://regexone.com/lesson/introduction_abcs
   * Reg Ex in Scripts: [[ STRING =~ REGEX]]
   
* sed (basic format) 
   * stands for stream editor.
   * Non-interactive text editor
   * By default output from sed goes to standard output
   * $ sed [options] commands [file-to-edit]
      * standard output
         * $ sed ‘’ file.txt
         * $ cat file.txt | sed ‘’
         * $ sed ‘p’ file.txt
            * P prints to standard output, but every line prints twice right now
         * $ sed –n ‘p’ file.txt
            * -n suppresses auto printing to standard output
       * specifying parts of the file
         * Choosing lines for sed to manipulate:
            * $ sed –n ‘1p’ file.txt #prints first line only
            * $ sed –n ‘1,5p’ file.txt #prints lines 1-5
            * $ sed -n ‘1,+4p’ file.txt #same result as above, but now we are specifying how many lines after the first
            * $ sed -n ‘1~2p’ file.txt #the 2 specifies every other line
      * deleting tes
         * Place ‘d’ for delete instead of ‘p’ for print in above examples.  Instead of printing, it will perform the corresponding delete.
         * Note that this has not permanently affected our file.  This is how you can and should text your expressions before making it permanent
      * saving changes
         * $ sed ‘’ file.txt > out.txt #good old redirection
         * $ sed –i ‘1d’ file.txt #-i sets IN PLACE editing, which means your file IS changed
         * $ sed –i.bak ‘1d’ file.txt #creates a backup of the original file ending with .bak
      * substitution format
         * Sed has the ability to search for text patterns using regular expressions, and then replace the found text
            * $ sed ‘s/old_stuff/new_stuff/’
               * Each slash (/) is a delimiter. You could use underscores (_) as delimeters as well.
            * $ sed ‘s/on/forward/’ file.txt
               * Replaces the first ‘on’ match with ‘forward’
            * $ sed ‘s/on/forward/g’ file.txt
               * Replaces every ‘on’ match with ‘forward’
            * $ sed ‘s/on/forward/gp’ file.txt
               * P at the end will have it only print lines that were affected
            * $ sed 's/^.*at/REPLACED/’ file.txt
               * Matches from beginning of line until ‘at’ is found, and substitutes all with ‘REPLACED’

* various ways to input / output from a file 
   * from powerpoint:
      * IO redirection using files
      * 'read' - will scan standard input
      * 'printf' - formats and prints
      * 'echo' - prints to standard output
      * Capture arguments:
         * $# where number is which argument you want to use
         * $@ - lets you access arguments as a list
         * So that you can use them in a loop, for example


### git
* init: git init initializes a repository
* clone
* **add**
* **commit**
* **push** : Pushes commits from my repo to the server
* **branch / checkout**
   * git checkout command lets you navigate between the branches created by git branch. 
   * Checking out a branch updates the files in the working directory to match the version stored in that branch, and it tells Git to record all new commits on that branch.

* **merge**
    * What step(s) should I take for a successful merge?
    * What does a merge do?
      * merge will combine multiple sequences of commits into one unified history. 
      * In the most frequent use cases, git merge is used to combine two branches.
      * Once Git finds a common base commit it will create a new "merge commit" that combines the changes of each queued merge commit sequence.

* pull (fetch + merge)
   * Pull is used to fetch and download content from a remote repository and immediately update the local repository to match that content.
   * Pull is really a combo of fetch followed by merge
* when to use a fork vs. a branch
    * fork - mostly for a full deviation from an original project
      *  When a branch needs to become it’s own thing (goes out of scope of the master branch), that’s when you should fork the project
      * Forks are commonly done when you see a useful start to your own project, and want to fork the primary project for a base of yours.
    * branch - mostly for features, useful for development streams

### virtualization
* virtual machines
    * what is a hypervisor? (week 11, slide 5)
      * Process that creates and runs VMs
      * Allows one host computer to support multiple guest VMs by virtually sharing its resources
      * Separates VMs from each other logically, assigning each its own slice of the underlying computing power, memory, and storage. 
      * This prevents the VMs from interfering with each other; so if, for example, one OS suffers a crash or a security compromise, the others survive.
      * When we have a host machine and install an additional application to run guest machines, we are using a Type 2 hypervisor
      * Type 1 hypervisors run are “bare metal” – they are the host

    * Install a full iso (including kernel)
    * Hypervisor virtualizes host machine's hardware
    * VMWare and VirtualBox
      * VirtualBox – by Oracle, pretty OpenSource, Windows, Mac, and Linux support
      * VMWare – Maybe owned by Dell now?  Smoother experience (entirely my opinion). Windows and Linux support


* containers
    * built from a recipe or build file
    * can run as an "image" or as a shell
    * relies on host OS kernel 
    * Docker and Singularity
      * Singularity implements a more secure version than Docker, so High Performance Computing systems focus on Singularity
      * In a Singularity container, your user identity is the same as on the host environment.  This makes sharing data between your home directory on the host and your container easy.  In fact, Singularity automatically mounts your home directory inside of the container.
      * Singularity also uses a single build or recipe file.  To transfer your environment to another person, they only need one file.
      * Docker is more everyday, so Singularity allows use of pre-built containers from Docker, but adds the security of Singularity.
    * require an underlying operating system that provides the basic services to all of the containerized applications using virtual-memory support for isolation


### networking 
* application layer
    * language that applications and servers use to communicate  
      * protocols include HTTP, SSL, FTP
    * web servers, ssh, file share
* transport / protocol layer
    * data transmission characteristics of applications  
    * TCP (Transmission Control Protocol) - handshake protocol where the connecting system and the system being connected to
        are constantly in communcation about recieving packets
    * UDP (User Datagram Protocol) - the connecting system is going to request information, and the system being connect to doesn't care if you got it or if was correct. Example - video chatting
    * Ports (and some common services on those common ports)
        * SSH or SFTP runs on port 22
        * HTTP runs on port 80 
        * HTTPS runs on port 443
* network / internet layer
    * how to move packets from a source to a destination
    * subnets - filter what is seen as "local" traffic
      * 10.23.2.0/24 = 255.255.255.0
      * subnet mask defines what is local traffic
    * routes
      * Definition: defines how traffic goes out and back in
      * $ route –n # displays routing table 
    * ip - outside of my system - assign to a system (we can base this on a MAC address for some hardware verification if wanted)
        * public ip - this would access global communcation 
        * private ip - usually behind a router that then allows communcation with the outside world
    * gateway
    * dns (hostname) -  DNS = Domain Name Service
      * Set a system hostname (for local system):
         * Windows: Powershell - Rename-Computer -NewName “NEW-PC-NAME”
         * Linux: Edit ‘/etc/hostname’ OR hostnamectl set-hostname “NEW-HOST-NAME”
    * dhcp: Dynamic Host Configuration Protocol
      * allows a device to automatically get its configuration from the network.
      * No manual entering of settings
      * No duplication of IPs
* physical layer
    * how to send raw data across physical medium
      * AKA Link layer or host-to-network layer
    * network interfaces (can be found with ifconfig in linux or with ipconfig in Windows)
        * Linux list these as eth0, wifi0, lo
        * Windows 
    * MAC addresses - these are "fingerprints" for hardware interfaces (or their vitrual counterparts)
* private networks (and their virtual counterparts)
* role of a router (virtual or physical)
    * directs traffic usually from a private network to a public network / server and back again
    * A router has more than one network interface.  
      * Yours at home should have a cable for getting to the world – this is called the internet uplink
    * most common private networks: 
      * 10.0.0.0 / 255.0.0.0
      * 192.168.0.0 / 255.255.0.0
      * 172.16.0.0 / 255.240.0.0

    * Router / gateway – a host on multiple subnets that routes traffic 
         * A router usually has a local subnet and a link to the internet
* role of firewalls locally (iptables) and by a specific device (for a network)
* http vs https - hypertext transfer protocol
    * HTTPS - digital certificates - from a certificate authority
        * encrypted connection between connecting system and server
        * Browser assumes it’s connected to the correct web server
        * Browser checks security certificate and verifies it comes from a legitimate certificate authority
         * Certificate Authority – the maintainers of the certificate keys.  Unlike the private / public keys we create, certificates for sites have an expiration date, then they need to be renewed.
        * People can’t see what you’re searching - they only get your primary URL

> You get an email with:
> IP: 130.108.67.34
> Subnet: 255.255.255.0
> Gateway: 130.108.67.1
> DNS: 130.108.23.24



Final Exam Details:
Open on Monday, 4/27, from 9:00 AM to 11:59 PM
You get two (2) hours from when you start the exam
You may use an electronic or printed "cheat sheet" as well as a terminal you have access to (including your AWS instance)
If I see the same words as are on my slides, much disappointment shall occur (and grade shall reflect)
