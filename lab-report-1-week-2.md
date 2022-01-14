# **SO YOU'RE TAKING CS15L**

Hello students of CS15L. It has come to my attention that you need some assistance in remote access.

Fret not, for in this tutorial, I will show you how to access your CS15L account and get started with remote acess.

---
## **Visual Studio Code**

One of the tools you need to get started will be Visual Studio Code. This is an IDE (Integrated development environment).
This is essentially the home base for all operations.

Go to [*this page*](https://code.visualstudio.com/) and download VSC for whatever operating system you are running on. If your system is not supported, let the staff know and they'll work out alternatives for you.


Your VSC should like something like this when you launch.

![VSCimage](https://i.gyazo.com/0c4fdc7b22111dcf36d8ffd82004f248.png)

---
## **Accessing your account**

In order to connect to a remote computer, you'll need access to your course-specific account.

> Firstly, if you're on windows, you need to install [**OpenSSH**](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse). This will allow you to connect to other computers that have the same type of account.

In order to get access to your course account, you'll need to look up your account [*here*](https://sdacs.ucsd.edu/~icc/index.php).

The page should look something like this, and you can fill out either field.

![AccountLookup](https://i.gyazo.com/fa3dcc93ae4e2d56a4366b6648894b4d.png)

Once you fill out the fields and click submit, you should be directed to a page with your associated accounts.

![Accounts](https://i.gyazo.com/0ff0203c82c0597cdd43c1cb73c1e7a0.png)

Click on the link that has CS15L - Quarter and Year - 3 random digits. In the above image it is the bottom one, cs15lwi22aep.

Once you have clicked on your 15L account, you should see a blue link to change your password.

![PasswordChange](https://i.gyazo.com/93a8b4746aa4f2dbd09f0421a845f1a1.png)

Click on this link, then fill out the form accordingly, keeping the same boxes checked as below.

![ChangePasswordPage](https://i.gyazo.com/def1de51846a5f30d346c809358fa231.png)

Once you have correctly filled out the form, you should be redirected to this page:

![DoneChangingPassword](https://i.gyazo.com/02949b8a147282a5f04f8b0862c42dfd.png)

Congratulations, you are now able to connect to your CS15L account using the password you set! Please give it some time to allow for the password change to take effect.

---
## **Connecting Remotely**

> Here is the guide in case you'd like to follow that instead: [https://code.visualstudio.com/docs/remote/ssh#_connect-to-a-remote-host](https://code.visualstudio.com/docs/remote/ssh#_connect-to-a-remote-host)

Now that your environment and account are ready to go, go into Visual Studio Code and open a terminal. This can be done by going to the top bar of the program, clicking on terminal, and clicking on new terminal. (This can also be done with the shortcut CTRL + SHIFT + ` )

It looks a little something like *this*:

![VSCTerminal](https://i.gyazo.com/644d94ecd9a053178272bbb4da6e6290.png)

Once your terminal is open, initiate the connection to a remote computer through the command :

`ssh cs15lwi22zz@ieng6.ucsd.edu`

where *wi22* will be replaced by your quarter (i.e. fa2023) and *zz* is replaced by your 15L account's letters.

Your terminal should look like this, including the warning message as you're accessing this for the first time:

```
⤇ ssh cs15lwi22zz@ieng6.ucsd.edu

The authenticity of host 'ieng6.ucsd.edu (128.54.70.227)' can't be established.
RSA key fingerprint is SHA256:ksruYwhnYH+sySHnHAtLUHngrPEyZTDl/1x99wUQcec.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

Don't worry about the warning, as again, you are connecting for the first time. If this message appears again even though you've connected to that specific host before, be careful. This [explanation](https://superuser.com/questions/421074/ssh-the-authenticity-of-host-host-cant-be-established/421084#421084) details why.

Now, it should prompt your password after you type and enter yes, and once you enter your password that you reset, you should be connected to a remote computer!

Here is the entire interaction:

```
⤇ ssh cs15lwi22aep@ieng6.ucsd.edu
Password: 
Last login: Thu Jan 13 09:06:52 2022 from 108-82-164-140.lightspeed.irvnca.sbcglobal.net
quota: No filesystem specified.
Hello cs15lwi22aep, you are currently logged into ieng6-203.ucsd.edu

You are using 0% CPU on this system

Cluster Status 
Hostname     Time    #Users  Load  Averages  
ieng6-201   18:30:01   30  2.26,  2.29,  2.33
ieng6-202   18:30:01   19  2.35,  2.37,  2.24
ieng6-203   18:30:01   14  1.89,  2.09,  1.92

 
Thu Jan 13, 2022  6:30pm - Prepping cs15lwi22
[cs15lwi22aep@ieng6-203]:~:2$ 
```

---

## **Testing Commands**

Now that you have succcessfully connected to a remote computer, it's time to try running some commands on the command line!

This is a time for you to toy around and try to understand commands, so have at it!

Commands to try:

- cd ~
- cd
- ls -lat
- ls -a
- ls `directory` where `directory` is /home/linux/ieng6/cs15lwi22/cs15lwi22abc, where *abc* is one of the other group members’ username
- cp /home/linux/ieng6/cs15lwi22/public/hello.txt ~/
- cat /home/linux/ieng6/cs15lwi22/public/hello.txt

Try running these commands on your computer and on the server.


>To log out of the server, use 
>- CTRL + D
>- Exit

Here is an example of some commands being ran:

![Commands](https://i.gyazo.com/11f2f8211e69c4c738782409c3d1f7f7.png)

---

## **Moving files with SCP**

Now that you've had some time to experiment with commands on the terminal, let's work on transferring files from one computer to the other. This is important as it is likely what you will be doing when working remotely.

To begin, we'll need the *scp* command. This should always be run on your computer (Log out of ieng6). To test this out, create a file on your computer called **WhereAmI.java**. Then, copy these contents into it:

```
class WhereAmI {
  public static void main(String[] args) {
    System.out.println(System.getProperty("os.name"));
    System.out.println(System.getProperty("user.name"));
    System.out.println(System.getProperty("user.home"));
    System.out.println(System.getProperty("user.dir"));
  }
}
```
> Skip this next step if you don't have java installed on your computer

Now, compile and run the program using *javac* and *java*. 

You should see your operating system, system username, home directory, and file directory.

It should look similar to this:

![WhereAmI.java](https://i.gyazo.com/7a0ef62dc58057e4d7b99d94d33e2308.png)

Now, in the same directory as the file you created, run this command in the terminal:

`scp WhereAmI.java cs15lwi22zz@ieng6.ucsd.edu:~/`

Again, you'll be prompted to enter your password. (Make sure to change the quarter and specific letters again)

Now, reconnect to the ieng6 computer and use the ls command to see the files. WhereAmI.java should be there, and you can compile and run it remotely!

Your terminal should look something like this:

![WhereAmITerminal](https://i.gyazo.com/452ad9e51cb3925664d9ae75db8ddf74.png)

---

## **Setting an SSH Key**

As you may have experienced, it is a pain to have to enter your password each time you try to remotely connect. The solution to that is an ssh key.

To begin, open the terminal and run the command:

`ssh-keygen`

It will begin to generate prompts, which you can just continuously press enter to end up with something like this:

```
# on client (your computer)
$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/joe/.ssh/id_rsa): /Users/joe/.ssh/id_rsa
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /Users/joe/.ssh/id_rsa.
Your public key has been saved in /Users/joe/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:jZaZH6fI8E2I1D35hnvGeBePQ4ELOf2Ge+G0XknoXp0 joe@Joes-Mac-mini.local
The key's randomart image is:
+---[RSA 3072]----+
|                 |
|       . . + .   |
|      . . B o .  |
|     . . B * +.. |
|      o S = *.B. |
|       = = O.*.*+|
|        + * *.BE+|
|           +.+.o |
|             ..  |
+----[SHA256]-----+
```

Now that your key has been generated, you need to copy the public key over to the ieng6 servers. To do this, connect to your course account.

```
$ ssh cs15lwi22zz@ieng6.ucsd.edu
Password:
# now on server
$ mkdir .ssh
$ exit
# back on client
$ scp /Users/username/.ssh/id_rsa.pub cs15lwi22zz@ieng6.ucsd.edu:~/.ssh/authorized_keys
# You use your username and the path you saw in the command above
```
Running these commands will allow you to be able to connect to your course account by just using ssh!

It should look similar to this when everything is done:

![SSHKeyImage](https://i.gyazo.com/ec653dd91148dbd7057228e7ad6786b6.png)

---

## **Optimizing remote running**

Now that you're able to automatically connect, you can make your life even easier by using tricks like these:

- You can write a command in quotes at the end of an ssh command to directly run it on the remote server, then exit.
- You can use semicolons to run multiple commands on the same line in most terminals.
- You can use the up-arrow on your keyboard to recall the last command that was run.

Here is an example where changes were made to WhereAmI.java, then sent to the course account and ran:

![RemoteEfficiency](https://i.gyazo.com/bea48c0fb6449dbbecfc95f368acce2a.png)

---

## **That's a wrap!**

I hope you were able to successfully follow this tutorial! If you get stuck anywhere, feel free to ask a TA for help. 

That's all, enjoy CS15L!