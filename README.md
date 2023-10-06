# openssh-server

A step-by-step guide on how to install OpenSSH server on an Ubuntu server, create an SSH key pair, and connect to the server from your Mac using SSH. Please note that you'll need administrative access to your Ubuntu server for these steps.

**Step 1: Install OpenSSH Server on Ubuntu Server**

1. Log in to your Ubuntu server using your username and password.

2. Open a terminal window.

3. Update the package list to ensure you have the latest package information:

   ```
   sudo apt update
   ```

4. Install the OpenSSH server package:

   ```
   sudo apt install openssh-server
   ```

5. The installation process will start, and you will be prompted to confirm by typing 'Y' if necessary.

6. Once the installation is complete, the SSH server should start automatically. You can check its status with:

   ```
   sudo systemctl status ssh
   ```

   It should show that the SSH server is active and running.

**Step 2: Create an SSH Key Pair on Your Mac**

1. Open a terminal on your Mac.

2. Use the following command to generate an SSH key pair. Replace `your_email@example.com` with your email address:

   ```
   ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
   ```

   This command will create an RSA key pair with a 4096-bit key length.

3. You will be prompted to choose a location to save the key pair. Press Enter to save it in the default location, which is usually `/Users/your_username/.ssh/id_rsa`.

4. You can optionally set a passphrase for added security. If you do, you will need to enter the passphrase every time you use the key.

**Step 3: Copy Your Public Key to the Ubuntu Server**

1. To copy your public key to the Ubuntu server, you can use the `ssh-copy-id` command. Replace `username` and `server_ip` with your server's username and IP address:

   ```
   ssh-copy-id username@server_ip
   ```

   You will be prompted to enter your server user's password.

2. Once the key is copied, you should be able to log in without a password from your Mac.

**Step 4: Connect to the Ubuntu Server from Your Mac**

1. To connect to your Ubuntu server from your Mac, use the `ssh` command. Replace `username` and `server_ip` with your server's username and IP address:

   ```
   ssh username@server_ip
   ```

   If you set a passphrase for your SSH key, you will be prompted to enter it now.

2. You should now be logged in to your Ubuntu server via SSH.


**Step 5: Copy Your Custom SSH Public Key to the Ubuntu Server**

1. On your host machine, open a terminal.

2. Use the `ssh-copy-id` command to copy your custom public key to your Ubuntu server. Replace `username`, `server_ip`, and `/path/to/your_custom_public_key.pub` with your server's username, IP address, and the path to your custom public key file:

   ```
   ssh-copy-id -i /path/to/your_custom_public_key.pub username@server_ip
   ```

   This command will copy your custom public key to the server's `~/.ssh/authorized_keys` file.

3. You will be prompted to enter your server user's password.

**Step 6: Connect to the Ubuntu Server Using Your Custom SSH Key**

1. On your host machine, open a terminal.

2. To connect to your Ubuntu server using your custom SSH key, use the `ssh` command. Replace `username` and `server_ip` with your server's username and IP address:

   ```
   ssh -i /path/to/your_custom_private_key username@server_ip
   ```

   Replace `/path/to/your_custom_private_key` with the actual path to your custom private key file.

3. If you have set a passphrase for your custom private key, you will be prompted to enter it.

4. You should now be logged in to your Ubuntu server using your custom SSH key pair.

Using `ssh-copy-id` with the `-i` option allows you to copy your custom SSH public key to the server's authorized keys file and then connect to the server using your custom private key.


That's it! You have successfully installed OpenSSH on your Ubuntu server, created an SSH key pair on your host machine, copied the public key to the server, and connected to the server using SSH without a password.
