# VM-SSH-Github

Generate a new SSH key on your VM machine and then add that generated key to your Github to give your VM SSH access to your Github repos.

In your terminal within your VM run the following command, replacing the email in the example with your Github email address:
```
ssh-keygen -t ed25519 -C "your_email@example.com"
```

This creates a new SSH key, using the provided email as a label.
You are then prompted to "Enter a file in which to save the key", you can press Enter to accept the default location.
```
> Generating public/private ALGORITHM key pair.
> Enter file in which to save the key (/c/Users/YOU/.ssh/id_ALGORITHM):[Press enter]
```
You are then prompted to create a passphrase which you can leave empty or enter in a secure passphrase.
```
> Enter passphrase (empty for no passphrase): [Type a passphrase]
> Enter same passphrase again: [Type passphrase again]
```

From your home directory navigate to your new .ssh file and create a config file.
```
cd .ssh
touch ~/.ssh/config
```

Open the new config file in a text editor or vim and add this text:
```
Host github.com
  AddKeysToAgent yes
  IdentityFile ~/.ssh/id_ed25519
```

Now run the following command to add your new SSH key to the ssh-agent:
```
ssh-add ~/.ssh/id_ed25519cd
```

Open the id_ed25519.pub file in a text editor or the built in vim editor of your terminal and copy the contents of that file.
It should start with ssh-ed25519 and end with your email.

On Github navigate to the settings menu by clicking your profile icon in the top right corner.
Within the settings menu locate the SSH and GPG keys option and click that.  
<img width="351" height="330" alt="image" src="https://github.com/user-attachments/assets/1f1f846e-1d58-47a5-8d2f-4bce15ad7115" />  
You will then click the green New SSH key.  
<img width="173" height="66" alt="image" src="https://github.com/user-attachments/assets/e9e51ec8-59f0-4a43-9819-bebbf52519af" />

Give your new SSH key a name and then past what you copied from your VM into the key box on Github.
You can use the same key to setup both Authentication as well as Signing but Authentication is the one that will let you remotely access your repositories.

When connecting your Github repos to your directories on you VM make sure to use the SSH option when getting the clone link.
It should look something like: ```git@github.com:Your_Username/Your_Repo.git```
Then proceed with connecting your local git to your github like normal with:
```
git remote add origin git@github.com:Your_Username/Your_Repo.git
git push -u origin master
```


