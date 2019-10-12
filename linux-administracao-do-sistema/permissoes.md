# Permissões

## chmod Lets You Change Read and Write Permissions in Linux[Permalink](https://linode.com/docs/tools-reference/tools/modify-file-permissions-with-chmod/?utm_source=Linode+Newsletters&utm_campaign=21f5a0277c-COMMUNITY_NEWSLETTER_Jan_2018&utm_medium=email&utm_term=0_68bafea72a-21f5a0277c-17266569#chmod-lets-you-change-read-and-write-permissions-in-linux) <a id="chmod-lets-you-change-read-and-write-permissions-in-linux"></a>

Unix-like systems, including the Linux systems that run on the Linode platform, have an incredibly robust access control system that allows systems administrators to effectively permit multiple users access to a single system without giving every user access to every file on the file system. The`chmod`command is the best and easiest way to modify these file permissions.

This guide provides a brief overview of file permissions and the operation of the`chmod`command in addition to a number of practical examples and applications of`chmod`. If you find this guide helpful, please consider our[basic administration practices guide](https://linode.com/docs/using-linux/administration-basics)and the[Linux users and groups guide](https://linode.com/docs/tools-reference/linux-users-and-groups/)next.

## How to Use chmod[Permalink](https://linode.com/docs/tools-reference/tools/modify-file-permissions-with-chmod/?utm_source=Linode+Newsletters&utm_campaign=21f5a0277c-COMMUNITY_NEWSLETTER_Jan_2018&utm_medium=email&utm_term=0_68bafea72a-21f5a0277c-17266569#how-to-use-chmod) <a id="how-to-use-chmod"></a>

In this guide,`chmod`refers to recent versions of`chmod`such as those provided by the GNU project. By default,`chmod`is included with all images provided by Linode, and as part of the common “base” selection of packages provided in nearly all distributions of Linux-based operating systems.

### Linux File Permission Basics[Permalink](https://linode.com/docs/tools-reference/tools/modify-file-permissions-with-chmod/?utm_source=Linode+Newsletters&utm_campaign=21f5a0277c-COMMUNITY_NEWSLETTER_Jan_2018&utm_medium=email&utm_term=0_68bafea72a-21f5a0277c-17266569#linux-file-permission-basics) <a id="linux-file-permission-basics"></a>

All file system objects on Unix-like systems have three main types of permissions: read, write, and execute access. Permissions are bestowed upon three possible classes: the user, the usergroup, and all system users.

To view the file permissions of a set of files, use:

```text
ls -lha
```

In the first column of the output, there are 10 characters that represent the permission bits. To understand why they are called permission bits, see the section on[octal notation](https://linode.com/docs/tools-reference/tools/modify-file-permissions-with-chmod/?utm_source=Linode+Newsletters&utm_campaign=21f5a0277c-COMMUNITY_NEWSLETTER_Jan_2018&utm_medium=email&utm_term=0_68bafea72a-21f5a0277c-17266569#octal-notation)below.

```text
drwxr-xr-x 2 user group       4.0K 2009-08-13 10:16 docs
-rw-r--r-- 1 user group       8.1K 2009-07-09 16:23 roster.py
lrwxrwxrwx 2 user group       4.0K 2009-08-13 10:16 team.docs
```

A way to understand the meaning of this column is to divide the bits into groups.

| File type | User | Group | Global |
| :--- | :--- | :--- | :--- |
| `d`Directory | `rwx` | `r-x` | `r-x` |
| `-`Regular file | `rw-` | `r--` | `r--` |
| `l`Symbolic Link | `rwx` | `rwx` | `rwx` |

The first character represents the type of file. The remaining nine bits in groups of three represent the permissions for the user, group, and global respectively. Each stands for:

* `r`

  :

  **R**

  ead

* `w`

  :

  **W**

  rite

* `x`

  : e

  **X**

  ecute

Note that access to files targeted by symbolic links is controlled by the permissions of the targeted file, not the permissions of the link object. There are[additional file permissions](https://linode.com/docs/tools-reference/linux-users-and-groups#additional-file-permissions)that control other aspects of access to files.

### chmod Command Syntax and Options[Permalink](https://linode.com/docs/tools-reference/tools/modify-file-permissions-with-chmod/?utm_source=Linode+Newsletters&utm_campaign=21f5a0277c-COMMUNITY_NEWSLETTER_Jan_2018&utm_medium=email&utm_term=0_68bafea72a-21f5a0277c-17266569#chmod-command-syntax-and-options) <a id="chmod-command-syntax-and-options"></a>

The format of a`chmod`command is:

```text
chmod [who][+,-,=][permissions] filename
```

Consider the following`chmod`command:

```text
chmod g+w ~/group-project.txt
```

This grants all members of the usergroup that owns the file`~/group-project.txt`write permissions. Other possible options to change permissions of targeted users are:

| Who \(Letter\) | Meaning |
| :--- | :--- |
| u | user |
| g | group |
| o | others |
| a | all |

The`+`operator grants permissions whereas the`-`operator takes away permissions. Copying permissions is also possible:

```text
chmod g=u ~/group-project.txt
```

The parameter`g=u`means grant group permissions to be same as the user’s.

Multiple permissions can be specified by separating them with a comma, as in the following example:

```text
chmod g+w,o-rw,a+x ~/group-project-files/
```

This adds write permissions to the usergroup members, and removes read and write permissions from the “other” users of the system. Finally the`a+x`adds the execute permissions to all categories. This value may also be specified as`+x`. If no category is specified, the permission is added or subtracted to all permission categories.

In this notation the owner of the file is referred to as the`user`\(e.g.`u+x`\).

```text
chmod -R +w,g=rw,o-rw, ~/group-project-files/
```

The`-R`option applies the modification to the permissions recursively to the directory specified and to all of its contents.

### How to Use Octal Notation for File Permissions[Permalink](https://linode.com/docs/tools-reference/tools/modify-file-permissions-with-chmod/?utm_source=Linode+Newsletters&utm_campaign=21f5a0277c-COMMUNITY_NEWSLETTER_Jan_2018&utm_medium=email&utm_term=0_68bafea72a-21f5a0277c-17266569#how-to-use-octal-notation-for-file-permissions) <a id="how-to-use-octal-notation-for-file-permissions"></a>

Another method for setting permissions is through octal notation.

Here is example of a file permission that is equivalent to`chmod u=rwx,go=rx`.

```text
chmod 750 ~/group-project.txt
```

The permissions for this file are`- rwx r-x ---`.

Disregarding the first bit, each bit that is occupied with a`-`can be replaced with a`0`while`r`,`w`, or`x`is represented by a`1`. The resulting conversion is:

```text
111 101 000
```

This is called octal notation because the binary numbers are converted to base-8 by using the digits 0 to 7:

| Binary | Octal | Permission |
| :--- | :--- | :--- |
| 000 | 0 | — |
| 001 | 1 | –x |
| 010 | 2 | -w- |
| 011 | 3 | -wx |
| 100 | 4 | r– |
| 101 | 5 | r-x |
| 110 | 6 | rw- |
| 111 | 7 | rwx |

Each digit is independent of the other two. Therefore,`750`means the current user can read, write, and execute while the group and others cannot write.

`744`, which is a typical default permission, allows read, write, and execute permissions for the owner, and read permissions for the group and “world” users.

Either notation is equivalent, and you may choose to use whichever form more clearly expresses your permissions needs.

## Making a File Executable[Permalink](https://linode.com/docs/tools-reference/tools/modify-file-permissions-with-chmod/?utm_source=Linode+Newsletters&utm_campaign=21f5a0277c-COMMUNITY_NEWSLETTER_Jan_2018&utm_medium=email&utm_term=0_68bafea72a-21f5a0277c-17266569#making-a-file-executable) <a id="making-a-file-executable"></a>

The following examples changes the file permissions so that any user can execute the file “~/group-project.py”:

```text
chmod +x ~/group-project.py
```

## Restore Default File Permissions[Permalink](https://linode.com/docs/tools-reference/tools/modify-file-permissions-with-chmod/?utm_source=Linode+Newsletters&utm_campaign=21f5a0277c-COMMUNITY_NEWSLETTER_Jan_2018&utm_medium=email&utm_term=0_68bafea72a-21f5a0277c-17266569#restore-default-file-permissions) <a id="restore-default-file-permissions"></a>

The default permissions for files on a Unix system are often`600`or`644`. Permissions of`600`mean that the owner has full read and write access to the file, while no other user can access the file. Permissions of`644`mean that the owner of the file has read and write access, while the group members and other users on the system only have read access.

Issue one of the following examples to achieve these “default” permissions:

```text
chmod 600 ~/roster.txt
chmod 644 ~/gigs.txt
```

For executable files, the equivalent settings would be`700`and`755`which correspond to`600`and`644`except with execution permission.

Use one of the following examples to achieve these executable “default” permissions:

```text
chmod 700 ~/generate-notes.py
chmod 755 ~/regenerate-notes.py
```

## Restrict File Access: Remove all Group and World Permissions[Permalink](https://linode.com/docs/tools-reference/tools/modify-file-permissions-with-chmod/?utm_source=Linode+Newsletters&utm_campaign=21f5a0277c-COMMUNITY_NEWSLETTER_Jan_2018&utm_medium=email&utm_term=0_68bafea72a-21f5a0277c-17266569#restrict-file-access-remove-all-group-and-world-permissions) <a id="restrict-file-access-remove-all-group-and-world-permissions"></a>

There are a number of cases where administrators and users should restrict access to files, particularly files that contain passwords and other sensitive information. The configuration files for msmtp and Fetchmail \(`~/.msmtprc`and`~/.fetchmailrc`\) are two common examples.

You can remove all access to these files with commands in one of the following forms:

```text
chmod 600 .msmtprc
chmod g-rwx,o-rwx .fetchmail
```

[https://linode.com/docs/tools-reference/tools/modify-file-permissions-with-chmod/?utm\_source=Linode+Newsletters&utm\_campaign=21f5a0277c-COMMUNITY\_NEWSLETTER\_Jan\_2018&utm\_medium=email&utm\_term=0\_68bafea72a-21f5a0277c-17266569](https://linode.com/docs/tools-reference/tools/modify-file-permissions-with-chmod/?utm_source=Linode+Newsletters&utm_campaign=21f5a0277c-COMMUNITY_NEWSLETTER_Jan_2018&utm_medium=email&utm_term=0_68bafea72a-21f5a0277c-17266569)

