---
title: Easy Rsync Remote Backups Using SSH Keys
author: Michael Schurter
layout: post
date: 2008-03-20
url: /2008/03/19/easy-rsync-remote-backups-using-ssh-keys/
dsq_thread_id:
  - 463870702
categories:
  - GNU/Linux
  - IT
  - Open Source
  - Technology
tags:
  - backups
  - keys
  - rsync
  - ssh

---
[Rsync][1] is an excellent file transfer utility thats especially well suited for backing up files over the Internet because it only transfers the data that has changed. A friend asked me how to set it up, so I thought I&#8217;d post what I sent him here.

**Goal:** Backup a directory from computer `Zim` to computer `Ark`

**Details:** 

  * Both `Zim` and `Ark` are subdomains of `example.com`
  * The user on `Ark` which receives the backup files is named `backupuser`
  * The user on `Zim` with access to the files you want to backup is named `steve`

**Prerequisites:**

  * [ssh][2] installed on both hosts
  * [rsync][3] installed on both hosts

  1. Login to `Zim` via `ssh`: <pre lang="bash">ssh steve@zim.example.com</pre>

  2. Generate a `ssh` key pair using: <pre lang="bash">ssh-keygen -t rsa
&lt;press enter when prompted where to save the key>
&lt;press enter twice when asked for a passphrase></pre>

  3. To use the key to login to `Ark` remotely without manually entering a password you need to copy the public key from `Zim` to `Ark` using: <pre lang="bash">ssh-copy-id -i .ssh/id_rsa.pub backupuser@ark.example.com</pre>
    
    If you don&#8217;t have `ssh-copy-id` on your system, get a new system. 😉 If thats not possible you can download the script with:
    
    <pre lang="bash">wget -O ssh-copy-id http://cvsweb.mindrot.org/index.cgi/~checkout~/openssh/contrib/ssh-copy-id?rev=1.6;content-type=text%2Fplain &#038;&#038; chmod +x ssh-copy-id</pre>
    
    Then retry the above command only you&#8217;ll need to prepend a &#8220;./&#8221;:
    
    <pre lang="bash">./ssh-copy-id -i .ssh/id_rsa.pub backupuser@ark.example.com</pre>

  4. Verify the key copied properly by attempting to login to `Ark`. You should _not_ be prompted for a password: <pre lang="bash">ssh backupuser@ark.example.com</pre>

  5. Logout of `Ark`. The key is setup, so you&#8217;re now ready to rsync files without having to manually enter a password.
  6. Test rsync by choosing a small file to backup and using: <pre lang="bash">rsync -tP /some/small/testfile backupuser@ark.example.com:/tmp</pre>
    
    A nice little progress bar should be displayed as the file is transferred. Confirm that &#8220;testfile&#8221; is now in `/tmp` on `Ark`.</li> 
    
      * You&#8217;re finally ready to do a real rsync like: <pre lang="bash">rsync -t /directory/to/backup/* backupuser@ark.example.com:/existing/backup/directory</pre>
        
        **Note:** There are several useful options for rsync. Check `man rsync` to find out more.
        
          * `-p` &#8212; preserve permissions (useful for backups, use -E if you only care about the executable bit)
          * `-r` &#8212; recursively backup directories.
          * `-z` &#8212; compressed uncompressed files
          * And just FYI: `-t` tells rsync to use the last modified timestamp to determine whether or not to transfer files. It makes rsync a _lot_ faster at determining whether or not files have changed.
      * To schedule the backup to take place nightly at 1:13 AM edit your crontab using `crontab -e` and insert the following line: <pre lang="bash">13 1 * * * rsync -qt /directory/to/backup/* backupuser@ark.example.com:/existing/backup/directory</pre></ol> 
    
    **Caveats:**
    
      * These instructions will _push_ files from `Zim` to `Ark`. There&#8217;s no reason why `Ark` couldn&#8217;t _pull_ files from `Zim`. In fact, this is often **more secure** if `Zim` is a web server with a larger attack surface than `Ark`. Mea culpa.
      * If the IP address of `Ark` is dynamic, use a service like [dyndns.com][4]. Otherwise SSH will give you errors.
      * _Major security warning:_ If someone breaks into `Zim`, they can also delete all of your backups on `Ark`. Never ever ever use the `root` user for backups on `Ark`. You can use the `root` user on `Zim` to send the backups, but its best to have a special backup user setup on `Ark` to receive the backup.

 [1]: http://www.samba.org/rsync/
 [2]: http://openssh.org/
 [3]: http://www.samba.org/rsync/download.html
 [4]: http://www.dyndns.com