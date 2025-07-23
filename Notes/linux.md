# Here I introduce the experiences when I learn to use VScode Remote SSH linux

1. Get the sudo right (you will be required to enter the password of your current user):
   ```linux
   sudo -i
   ```
   ```linux
   sudo cd /home/abc
   ```

2. Next you will see the root user, and then you can enter your commend:
   ```linux
   root@ubuntu:~#
   ```

3. Check all the users:
   ```linux
   getent group
   ```

4. Check whether there is such file or directory (linux systems are case sensitive):
   ```linux
   ls /home/wzx
   ```

5. Check the current environment variable of your path:
   ```
   echo $PATH
   ```

6. Use cd commend to enter the directory of other users:
   ```
   sudo -i
   ```
   ```
   cd /usr/bin
   ```

