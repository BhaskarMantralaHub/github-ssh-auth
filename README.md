# Github SSH (Secure Shell Protocol)

## Generating a new SSH key
On Mac :computer:

```sh
ssh-keygen -t ed25519 -C "GITHUB_EMAIL_ADDRESS"

Generating public/private ed25519 key pair.

Enter file in which to save the key (/Users/<>/.ssh/id_ed25519):

Created directory '/Users/<>/.ssh'.
```

## Enter Passphrase

> Enter passphrase for additional security
```sh
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
```
**Response**:
```sh
Your identification has been saved in /Users/<>/.ssh/id_ed25519

Your public key has been saved in /Users/<>/.ssh/id_ed25519.pub
```

## Start ssh-agent
```sh
eval "$(ssh-agent -s)"
```
**Response:**

```sh
Agent pid <>
```

## Adding your SSH key to the ssh-agent

* ssh-agent to manage your keys
* Add ssh key to ssh-agent using `ssh-agent`
* Create `~/.ssh/config` to automatically loads keys into ssh-agent

>  Add the following to ~/.ssh/config
 ```sh
Host github.com
	  AddKeysToAgent yes
	  UseKeychain yes
	  IdentityFile ~/.ssh/id_ed25519
```

> If passphrase is added, then AddKeysToAgent must be yes

## Add your SSH private key to the ssh-agent and store your passphrase in the keychain

```sh
ssh-add --apple-use-keychain ~/.ssh/id_ed25519
```

> `--apple-use-keychain` option stores the passphrase in your keychain

## Add public key to Github

* Get the public key using below command and copy the output:
  ```sh
   cat ~/.ssh/id_ed25519.pub
   ```
* From github settings / SSH and GPG keys / New SSH Key
* Add key name and paste the public key
* Save the key
* Now, start using SSH
