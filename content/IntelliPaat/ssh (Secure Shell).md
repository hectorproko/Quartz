Protocol used for secure remote access and file transfer.

# .ssh (directory)
  - This is a directory typically located in a user's home directory (e.g., `~/.ssh/`).
  - The directory itself usually has strict permissions to ensure security (`drwx------` or `700` in octal representation).


# known_hosts (file)
- A file inside the `.ssh` directory (i.e., `~/.ssh/known_hosts`).
- It keeps a record of remote hosts a user has connected to via SSH.
- When you connect to a remote server for the first time, you're presented with its public key fingerprint and asked to verify its authenticity. If you accept, the server's identification is saved in the `known_hosts` file.
- This file helps in preventing man-in-the-middle attacks by ensuring you're connecting to the server you intend to.

# [[authorized_keys]] (file)
- Another file inside the `.ssh` directory (i.e., `~/.ssh/authorized_keys`).
- It contains a list of public keys that are allowed to authenticate to the user's account.
- To set up SSH login without a password using public key authentication, you add the public key from the connecting machine to the `authorized_keys` file on the target machine you're trying to access.
- If the private key corresponding to any of the public keys in this file is presented during authentication, the SSH server allows the connection without a password.

> [!tip]
> When a machine tries to establish an SSH connection using public key authentication:
> 
> 1. The connecting machine presents its private key to prove its identity.
> 2. The target machine checks its `authorized_keys` file to see if it has a corresponding public key for that private key.
> 3. If a match is found, the connection is authenticated without needing a password.
> 
> So, to rephrase the statement:
> 
> "If the connecting machine presents a private key that matches any of the public keys in the `authorized_keys` file of the target machine, the SSH server permits the connection without requesting a password."


generate key:
```bash
ssh-keygen
```

