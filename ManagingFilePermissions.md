<h1>Managing File Permissions in Linux</h1>

<h2>Project description</h2>
As a security professional at a large organization, part of my job is to ensure users on the team are authorized with appropriate permissions. The assigned task is to examine existing permissions on the file system and determine if the permissions match the authorization that should be given. If they do not match, I need to modify the permissions to authorize the appropriate users and remove any unauthorized access:

<h2>Check file and directory details</h2>
The command to use to check file and directory details is <code>ls</code>, with the arguments <code>l</code> (for permissions) and <code>a</code> (to include hidden files):
 
![Linux01](https://github.com/user-attachments/assets/6c41d986-4b7b-4b75-9514-d896d150ada2)


<h2>Describe the permissions string</h2>
As an example, we will describe the read/write/execute permissions string for project_t.txt. The permissions are denoted as r, w, and x respectively.
The permissions string is -rw-rw-r--.
The first character represents the file type. A hyphen (-) denotes that it is a file, and a d denotes that it is a directory. The second to fourth characters represent permissions for the user who owns the file, the fifth to seventh characters represent permissions for the group, and the eighth to tenth characters represent permissions for other users. A hyphen (-) in the second to tenth characters denotes the lack of permission for the file. Therefore, for the file project_t.txt, the owner has read and write permissions, group also has read and write permissions, and other users have only read permissions.

<h2>Change file permissions</h2>
The organization does not allow other to have write permissions to any files, so we need to modify the permissions accordingly: 

![Linux02](https://github.com/user-attachments/assets/adca23cd-1c92-44bb-b21a-3665cde3ef48)

We know from the previous screenshot that other has write permissions to only project_k.txt, so we used chmod to remove this permission.
chmod is used to change file or directory permissions.
In the first argument "o-w", "o" indicates that other needs permissions changed, "-" indicates that permission(s) need to be removed ("+" would mean to add a permission), and "w" indicates that write permission needs to be added.
The second argument is the name of the file for which we are changing permissions, project_k.txt.
There is no output to this command, but the change takes place successfully.

<h2>Change file permissions on a hidden file</h2>
The team has archived .project_x.txt, which is why it’s a hidden file (hidden files and directories are denoted by a "." at the beginning). This file should not have write permissions for anyone, but the user and group should be able to read the file. From the first screenshot, we know that .project_x.txt has write permissions for user and group, and read permissions for user. To set permissions so that only the user and group has read permissions but not write permissions, we use the command chmod u=r,g=r .project_x.txt, where the "=" overwrites previous permissions to the ones that follow:

 ![Linux03](https://github.com/user-attachments/assets/ca5a9163-48e9-4bdd-bde9-b7da384be99c)

<h2>Change directory permissions</h2>
The files and directories in the projects directory belong to the researcher2 user. Only researcher2 should be allowed to access the drafts directory and its contents. To modify the permissions accordingly, we simply need to remove execute permission for the group by using the command chmod g-x drafts:

![Linux04](https://github.com/user-attachments/assets/d0ffd096-c68e-4bb1-bb84-e3a7e678701f)
 
<h2>Summary</h2>
Using the Linux Bash Shell, this document outlined how to execute basic commands related to examining file and directory permissions, change permissions on files (including hidden files), and change permissions on directories. This enhances the security of the organization by using the principle of least privilege and only granting only minimal access and authorization required to complete a task or function.
