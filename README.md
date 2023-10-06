
A step-by-step guide on how to install OpenSSH server on an Ubuntu server, create an SSH key pair, add your custom SSH key to the SSH agent on your Mac, and connect to the server from your Mac using SSH with passwordless authentication. Please note that you'll need administrative access to your Ubuntu server for these steps.

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
6. Once the installation is complete, the SSH server should start automatically. However, to ensure it's enabled to start on boot, use the following command:
   ```
   sudo systemctl enable ssh
   ```
7. Once the installation is complete, the SSH server should start automatically. You can check its status with:

   ```
   sudo systemctl status ssh
   ```

   It should show that the SSH server is active and running.

**Step 2: Create an SSH Key Pair on Your Mac**

1. On your Mac, open a terminal.

2. Use the following command to generate an SSH key pair. Replace `your_email@example.com` with your email address:

   ```
   ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
   ```

   This command will create an RSA key pair with a 4096-bit key length.

3. You will be prompted to choose a location to save the key pair. Press Enter to save it in the default location, which is usually `/Users/your_username/.ssh/id_rsa`.

4. You can optionally set a passphrase for added security. If you do, you will need to enter the passphrase every time you use the key.

**Step 3: Add Your SSH Key to the SSH Agent on Your Mac**

1. On your Mac, open a terminal.

2. Start the SSH agent by running the following command:

   ```
   eval "$(ssh-agent -s)"
   ```

3. Add your private key to the SSH agent:

   ```
   ssh-add ~/.ssh/id_rsa
   ```

   If you set a passphrase for your key, you will be prompted to enter it.

4. Verify that your SSH key has been added to the agent:

   ```
   ssh-add -l
   ```

   You should see your key listed.

**Step 4: Copy Your Public Key to the Ubuntu Server**

1. To copy your public key to the Ubuntu server, you can use the `ssh-copy-id` command. Replace `username` and `server_ip` with your server's username and IP address:

   ```
   ssh-copy-id username@server_ip
   ```

   You will be prompted to enter your server user's password.

2. Once the key is copied, you should be able to log in without a password from your Mac.

**Step 5: Connect to the Ubuntu Server from Your Mac**

1. To connect to your Ubuntu server from your Mac, use the `ssh` command. Replace `username` and `server_ip` with your server's username and IP address:

   ```
   ssh username@server_ip
   ```

   If you set a passphrase for your SSH key, you will be prompted to enter it now.

2. You should now be logged in to your Ubuntu server via SSH.

**Step 6: Disable Password Authentication on the Ubuntu Server (Optional)**

1. On your Ubuntu server, open a terminal.

2. Edit the SSH server configuration file (`sshd_config`) using a text editor:

   ```sh
   sudo nano /etc/ssh/sshd_config
   ```

3. Locate the following line:

   ```
   #PasswordAuthentication yes
   ```

   Uncomment this line (remove the `#` at the beginning) and set it to `no`:

   ```
   PasswordAuthentication no
   ```

   This change will disable password-based authentication for SSH on your server.

4. Save the changes and exit the text editor.

5. Restart the SSH service to apply the changes:

   ```sh
   sudo systemctl restart ssh
   ```

**Step 7: Test SSH Key-Based Authentication**

1. On your Mac, open a terminal.

2. To connect to your Ubuntu server using SSH, use the `ssh` command as before:

   ```sh
   ssh username@server_ip
   ```

   You should now be able to log in without being prompted for a password or passphrase. SSH key-based authentication is enabled, and password-based authentication is disabled for added security.

By following these steps, you've installed OpenSSH on your Ubuntu server, created an SSH key pair on your Mac, added your custom SSH key to the SSH agent, copied the public key to the server, and connected to the server using SSH without a password. Additionally, you have the option to disable password-based authentication on the server for enhanced security.
