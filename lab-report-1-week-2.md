# Lab Report Week 2

*Abhishek Govindarasu*


![Image](https://scitechdaily.com/images/Illustration-Photons-Galaxy-777x518.jpg)

## How to Login to ieng6 Servers
> 1. Install VSCode
>> Download VSCode [here](https://code.visualstudio.com/download)
>> ![VSCode](vscode_1.png)
> 2. Login via SSH
>> ```bash
>> ssh cs15lwi22zzz@ieng6.ucsd.edu
>> ```
> 3. Use Unix Commands on ieng6 Server
>> Type ```help``` for system unix commands
>> ![Example](files_2.png)
> 4. Using scp to transfer files
>> ![SCP](scp_move_3.png)
>> ```bash
>> scp file cs15lwi22zzz@ieng6.ucsd.edu:~/
>> ```
> 5. SSH Keys
>> ```bash
>> ssh-keygen
>> ```
>> Now login without password
>> ![Login](login_key.png) 
> 6. Optimization
>> ```bash
>> scp file.java cs15lwi22zzz@ieng6.ucsd.edu:~/; ssh cs15lwi22zzz@ieng6.ucsd.edu "javac file.java; java file"
>> ```





