# 4.3. [Adding the LFS User](http://www.linuxfromscratch.org/lfs/view/stable/chapter04/addinguser.html)

### As root, issue the following commands to add the new user:
```bash
groupadd lfs
useradd -s /bin/bash -g lfs -m -k /dev/null lfs
```
* `-s /bin/bash`: This makes bash the default shell for user lfs.
* `-g lfs`: This option adds user lfs to group lfs.
* `-m`: This creates a home directory for lfs.
* `-k /dev/null`: This parameter prevents possible copying of files from a skeleton directory (default is /etc/skel) by changing the input location to the special null device.
* `lfs`: This is the actual name for the created group and user.

### To log in as lfs (as opposed to switching to user lfs when logged in as root, which does not require the lfs user to have a password), give lfs a password:
`passwd lfs`

### Grant lfs full access to $LFS/tools by making lfs the directory owner:
`chown -v lfs $LFS/tools`

### If a separate working directory was created as suggested, give user lfs ownership of this directory:
`chown -v lfs $LFS/sources`

### Next, login as user lfs. This can be done via a virtual console, through a display manager, or with the following substitute user command:
`su - lfs`



# 4.4. [Setting Up the Environment](http://www.linuxfromscratch.org/lfs/view/stable/chapter04/settingenvironment.html)
