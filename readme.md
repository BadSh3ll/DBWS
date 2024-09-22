# DBWS COURSE MANUAL

## Introduction

This manual is intended to provide a comprehensive guide to the Database and Web Services course. The manual is divided into several sections, each covering a different aspect of the course.

## Table of Contents

<!-- ssh, git, and mysql -->

1. [SSH](#ssh)
2. [Git](#git)
3. [MySQL](#mysql)

## SSH

SSH, or Secure Shell, is a cryptographic network protocol used for secure communication between two computers. It is widely used for remote login and command execution, file transfer, and tunneling.

### Connecting to a Remote Server (Linux/Mac)

To connect to a remote server using SSH, you can use the following command:

```bash
ssh username@5.75.182.107
```

Replace `username` with your username and enter the password when prompted.

If you are tired of typing the ip address every time you want to connect to the server, you can add an entry to your `/etc/hosts` file:

```bash
echo "5.75.182.107 teaching" | sudo tee -a /etc/hosts
```
Then you can connect to the server using the hostname:

```bash
ssh username@teaching
```

### Connecting to a Remote Server (Windows)

To connect to a remote server using SSH on Windows, you can use a tool like PuTTY or PowerShell (The commands are similar to Linux/Mac).

### Generating SSH Keys

If you want to connect to a remote server without entering a password every time, you can generate SSH keys and add them to the server's `authorized_keys` file.

To generate SSH keys, you can use the following command:

```bash
ssh-keygen
```

This will generate a public and private key pair in the `~/.ssh` directory. The name of the keys could be (id_rsa, id_rsa.pub) or (id_ed25519, id_ed25519.pub), ... etc. Depending on the algorithm.

To copy the public key to the server, you can use the following command:

```bash
ssh-copy-id username@teaching
```

Or you can manually copy the public key to the server's `authorized_keys` file.

```bash
cat ~/.ssh/id_rsa.pub | ssh username@teaching "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```

## Git

Git is a distributed version control system used for tracking changes in source code during software development. It is designed to handle everything from small to very large projects with speed and efficiency.

### Create a git repository

In order to manage your project and keep track of the submissios, your team needs to have a git repository. 

**And the reposity must be hosted on the teaching server.**

### Steps

1. Create a new repository on the server

```bash
# Just for team leaders
# On the server
git init --bare /path/to/project
```

2. All others members generate a ssh key and send it to the team leader

```bash
# From team members
# On the local laptop
ssh-keygen # Skip if you already have a key
cat ~/.ssh/id_rsa.pub
```

3. The team leader adds the public key to the server

```bash
# From team leader
# On the server
echo "<copied_public_key>" >> ~/.ssh/authorized_keys
```

4. Clone the repository

```bash
# From team members
# On the local laptop
git clone <leader_username>@teaching:/path/to/project
```

5. Add, commit, and push your changes

```bash
# On the local laptop
git add .
git commit -m "Your message" # For example: "Assignment #2 submission"
git push origin main
```

## MySQL

MySQL is an open-source relational database management system. It is widely used in web applications to store and retrieve data.

### Connecting to MySQL

To connect to a MySQL database, you can use the following command:

```bash
# On the server
mysql -u <username> -p<password>
```

You can then see your associated databases:

```sql
SHOW DATABASES;
```
Your output should look like this:

````
MariaDB [(none)]> show databases;
+--------------------+
| Database           |
+--------------------+
| <username>_db      |
| information_schema |
+--------------------+
2 rows in set (0.001 sec)
````

You can then select your database to start working on it:

```sql
USE <username>_db;
```

After that, you can start creating tables, inserting data, and querying data.

