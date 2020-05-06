# Rakete
![GitHub tag (latest SemVer)](https://img.shields.io/github/v/tag/ericvilla/rakete?sort=semver) [![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)

**Rakete** is a tool that provides you an easy way to deploy a .zip archive to a remote host and to issue commands to the remote host once the .zip archive is uploaded.
Rakete should be run from the directory you want to compress the content of.
Rakete uses **scp** to upload the .zip archive from the local to the remote host. Once the upload is completed, a preconfigured list of commands are executed on the server using a simple **ssh** session.

## Installation
Download:
```
curl https://raw.githubusercontent.com/ericvilla/rakete/master/rakete -o /usr/local/bin/rakete
```
Set permissions:
```
chmod +x /usr/local/bin/rakete
```

## Configuration
Before you can properly use Rakete, you should configure a **.rakete** directory inside you project directory.
This directory should contain two configuration files:
- **vars.yml**, containing the variables needed to upload the .zip archive correctly;
- **cmds.yml**, containing a list of commands that will be issued to the remote host once the .zip archive is uploaded.

### vars.yml
```
ssh_key: /Users/johndoe/Keys/my-key.pem
local_user: johndoe
local_folder: /Users/johndoe/Projects/my-project
local_zip_folder: /Users/johndoe
remote_user: ubuntu
remote_zip_folder: /path/to/zip/folder
remote_folder: /path/to/folder
```

> **NOTE:** each of this variable should be present in order to make Rakete work properly.

### cmds.yml

```
cmds:
  - 
    desc: <COMMAND-1-DESCRIPTION>
    cmd: <COMMAND-1>
  - 
    desc: <COMMAND-2-DESCRIPTION>
    cmd: <COMMAND-2>
  - 
    desc: <COMMAND-3-DESCRIPTION>
    cmd: <COMMAND-3>
```

 > **NOTE:** you should define a "cmds" key. The value of the "cmds" key should be an array of objects, 
 > each of which contains a "desc" and a "cmd" key. The "desc" key's value corresponds to the description
 > of the command while the "cmd" key's value corresponds to the command that will be executed on the
 > remote instance. Remember to prepend an escape character to every "$" character that appears in your
 > commands, otherwise it will be evaluated!

 ### Usage

 From your terminal, move to your project directory. If you have already configured the .rakete folder and you know your remote host's IP address or hostname, type the following command:

 
 ```
 rakete -r <REMOTE-HOST-IP-ADDRESS-OR-HOSTNAME>
 ```

Rakete will create a .zip archive from your project directory, upload it to the remote host and issue the previously configured commands to the remote host.
