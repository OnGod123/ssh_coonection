Step-by-Step Guide for Setting Up SSH Key-Based Authentication
1. Generate a New SSH Key Pair (If Not Already Done)
If you don't already have an SSH key pair, generate one:

bash
Copy code
ssh-keygen -t rsa -b 4096 -f ~/.ssh/school
This will create two files:

~/.ssh/school (private key)
~/.ssh/school.pub (public key)
2. Manually Copy the Public Key to the Server
Print the contents of the public key:

bash
Copy code
cat ~/.ssh/school.pub
Log in to the server using password authentication:

bash
Copy code
ssh ubuntu@your_server_ip
Create the .ssh directory and authorized_keys file if they don't exist:

bash
Copy code
mkdir -p ~/.ssh
chmod 700 ~/.ssh
touch ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
Append the public key to the authorized_keys file:
On your local machine, copy the output from cat ~/.ssh/school.pub. Then, on the server, run:

bash
Copy code
echo "your-public-key-contents" >> ~/.ssh/authorized_keys
Replace your-public-key-contents with the actual contents from the cat ~/.ssh/school.pub command output.

Ensure the permissions are set correctly:

bash
Copy code
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
Exit the server:

bash
Copy code
exit
3. Test the SSH Connection
Test the SSH connection using the private key:

bash
Copy code
ssh -i ~/.ssh/school ubuntu@your_server_ip
Confirm the host fingerprint:
When prompted, type yes to add the server's host key to your known_hosts file.

4. Create a Script for Easy Access
Create the script:

bash
Copy code
nano 0-use_a_private_key
Add the following content to the script:

bash
Copy code
#!/bin/bash

# Define the server's IP address or hostname
SERVER="your_server_ip"

# Use ssh with single-character flags to connect to the server
ssh -i ~/.ssh/school ubuntu@$SERVER
Save and exit the editor (CTRL+X, Y, Enter).

Make the script executable:

bash
Copy code
chmod +x 0-use_a_private_key
Run the script:

bash
Copy code
./0-use_a_private_key
Summary
Generate SSH key pair (if needed).
Manually copy the public key to the server's authorized_keys file.
Test the connection using the private key.
Create a script for easy future access.
Explanation
Generating the key pair: You need a private and a public key. The private key stays on your machine, and the public key goes to the server.
Copying the public key: By copying the public key to the ~/.ssh/authorized_keys file on the server, you enable the server to authenticate your private key.
Testing the connection: Ensures everything is set up correctly.
Creating a script: Simplifies future connections.
By following these steps, you ensure that the server can correctly authenticate your SSH connection using the public key you've provided.


