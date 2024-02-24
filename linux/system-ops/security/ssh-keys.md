# SSH Keys

## <mark style="color:red;">Generate Keys</mark>

`ssh-keygen -t rsa -b 2048 -C "your_email@example.com"`

Key Type `-t`: \
<mark style="color:orange;">**rsa**</mark>: RSA key type. \
<mark style="color:orange;">**dsa**</mark>: DSA key type. \
<mark style="color:orange;">**ecdsa**</mark>: ECDSA key type. \
<mark style="color:orange;">**ed25519**</mark>: Ed25519 key type.

Key Length (`-b`): \
Specify the number of bits in the key.

Comment (`-C`): \
Add a comment to identify the key (usually an email address).

Output File (`-f`): \
Specify the filename for the key pair.

Passphrase (`-N`): \
Set a passphrase to protect the private key.

Passphrase (`-P`): \
Requests changing the passphrase of a private key file instead of creating a new private key. \
The program will prompt for the file containing the private key, for the old passphrase, and twice for the new passphrase.

Key Location: \
By default, keys are saved in \~/.ssh/ directory.

`ssh-keygen -t rsa -b 2048 -C "john.doe@example.com" -f ~/.ssh/id_rsa`\
This command generates an RSA key pair with a key length of 2048 bits and a comment of "john.doe@example.com". \
The keys will be saved as id\_rsa (private key) and id\_rsa.pub (public key) in the \~/.ssh/ directory.

## <mark style="color:red;">Steal Keys</mark>

### <mark style="color:purple;">Find Private Keys</mark>

| Command                                    | Description                                  |
| ------------------------------------------ | -------------------------------------------- |
| `find / -name id_rsa`                      | System-wide search for key by name.          |
| `locate id_rsa`                            | Searches for key using the `locate` command. |
| `grep -r -l "BEGIN RSA PRIVATE KEY" /etc/` | Search /etc/ for keys                        |
| `find ~/.ssh -name "id_rsa*" -type f`      | Search in home dir                           |
| `find /etc/ssh -name "id_rsa*" -type f`    | Search for system-wide keys                  |

### <mark style="color:purple;">Find Public Keys</mark>

| Command                                   | Description                                        |
| ----------------------------------------- | -------------------------------------------------- |
| `find / -name "*.pub"`                    | System-wide search for key files by name.          |
| `locate "*.pub"`                          | Searches for key files using the `locate` command. |
| `grep -r -l "ssh-rsa" /etc/`              | Search /etc/ for keys                              |
| `find ~/ -name "[filename].pub" -type f`  | Search in home dir                                 |
| `find ~/.ssh -name "id_rsa*.pub" -type f` | Search in home dir                                 |

Display SSH host key information: \
`ls -l /etc/ssh/ssh_host*`

Look for .ssh and see if you can get the private key.

If you can, copy it to your attack box. Then change it's permissions:\
`chmod 600 root_key`

Use the key to log in to that user that it belongs to.\
`ssh -i root_key -oPubkeyAcceptedKeyTypes=+ssh-rsa -oHostKeyAlgorithms=+ssh-rsa [user]@[targetIP]`
