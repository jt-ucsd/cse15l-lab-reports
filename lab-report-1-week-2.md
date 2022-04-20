# Lab Report 1
By: jt

## Installing VSCode
---
1)	Download and install VSCode.  You will need to go to their [website](https://code.visualstudio.com/download) and download the appropriate file for your computer.  Afterwards, install VSCode like any other program.

![VSCode Install](https://raw.githubusercontent.com/jt-ucsd/cse15l-lab-reports/main/VSCode%20Download%20Website.jpg)

## Remotely Connecting
---
1) Launch VSCode.  Navigate to Terminal and click “Create a New Terminal”.  Type in cs15lsp22zz@ieng6.ucsd.edu into the terminal.  The terminal will prompt you for a password and you will need to either reset your old password (if it doesn’t work) or use the one you already set.

   Note: zz are placeholders, you have a unique combination of letters that should replace the zz.  You can find your account on TritonLink Account Finder.  To find the letters go to https://sdacs.ucsd.edu/~icc/index.php and look for a CS 15L account.

![VSCode Terminal Login](https://raw.githubusercontent.com/jt-ucsd/cse15l-lab-reports/main/Password%20Prompting.jpg)

2) If you logged in successfully.  It should look like this.

![SSH Login](https://raw.githubusercontent.com/jt-ucsd/cse15l-lab-reports/main/Successful%20Login.jpg)

## Trying some Commands
---
1)	You can run some linux commands through ssh.  Try doing `$ ls`, which will list all the files and the directory.  If you are ever stuck, you can type `$ man` to access the manual page or `$ man [command]` if you want to access the manual on a specific command.

![SSH Terminal Commands](https://raw.githubusercontent.com/jt-ucsd/cse15l-lab-reports/main/Command%20Running.jpg)

## Moving files with `scp`
---
1)	We can also try copying a file from your computer to the remote computer.  Create a new java file in VS Code and copy the following code.

```
class HelloWorld {
   public static void main(String[] args) {
      System.out.println(System.getProperty("os.name"));
      System.out.println("Hello World!")
   }
}
```

![Java File Coded](https://raw.githubusercontent.com/jt-ucsd/cse15l-lab-reports/main/Java%20File%20Opened.jpg)

2) Then, open up your terminal again.  It should be back to your computer terminal.  Redirect to the folder containing the java file using `# cd` and type `scp HelloWorld.java cs15lsp22zz@ieng6.ucsd.edu:~/`.  Once again, it will prompt you to type in your password and you will type it in.  If done correctly, it will show the screen below.

![SCP Successful](https://raw.githubusercontent.com/jt-ucsd/cse15l-lab-reports/main/Successful%20Copy.jpg)

3) Now, log into ssh as taught earlier and type in `$ ls`.  You will now see a file called HelloWorld.java.  This is the file that you copied over.  You can type `$ javac HelloWorld.java` and `$ java HelloWorld.java` to run the program.

![Running Java on SSH](https://raw.githubusercontent.com/jt-ucsd/cse15l-lab-reports/main/Running%20Copied%20Over%20Java%20File.jpg)

## Setting up an SSH Key
---
1) Install and run PowerShell.  You will need to run `# Start-Service ssh-agent`, followed by `# Get-Service ssh-agent`, which should tell you that it is running.

![Running Java on SSH](https://raw.githubusercontent.com/jt-ucsd/cse15l-lab-reports/main/PowerShell%20SSH%20Agent%20Running.jpg)

2) Now, on PowerShell, type `ssh-keygen` and just use the default for everything.  When it prompts to enter a passphrase, just hit return so you don't have to type in a password.  If you did this correctly, you will find two files created in `users/username/.ssh`

![Running Java on SSH](https://raw.githubusercontent.com/jt-ucsd/cse15l-lab-reports/main/PowerShell%20Keygen.jpg)


3) Now you will need to copy the public key called id_rsa.pub by using `scp id_rsa.pub cs15lsp22zz@ieng6.ucsd.edu:~/.ssh/authorized_keys`.  Remember to redirect to the folder.  Afterwards, try to login again and you won't need to use your password.

![Using SSH Key](https://raw.githubusercontent.com/jt-ucsd/cse15l-lab-reports/main/SCP%20Success.jpg)

## Optimizing Remote Running
---
1) You can optimize remote running by combining multiple commands into one line.  A `;` will allow you to run multiple commands on the same line for most terminals while a `"` lets you run commands remotely on the server.  It saves time as you don't have to enter each one line by line and wait.

Example Optimization: `scp HelloWorld.java cs15lsp22atu@ieng6.ucsd.edu:~/; ssh cs15lsp22atu@ieng6.ucsd.edu "ls; javac HelloWorld.java; java HelloWorld"`

![Example of MultiLine Command](https://raw.githubusercontent.com/jt-ucsd/cse15l-lab-reports/main/SSH%20Multiline%20Command.jpg)
