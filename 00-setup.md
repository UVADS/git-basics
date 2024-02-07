# Set Up & Install Git

Setting up git and authenticating yourself to GitHub is an important first step in managing and tracking your code and various projects. Follow these steps, in order:

<ol style="list-style-type: decimal;">
    <li>Install Git using the instructions at the following link. A git GUI version is optional, but the command line version is required for this course: <a href="https://git-scm.com/book/en/v2/Getting-Started-Installing-Git" target="_blank" rel="noopener">https://git-scm.com/book/en/v2/Getting-Started-Installing-Git</a>&nbsp;</li>
    <li>Check that git is installed in your environment by issuing the <code>git</code> command.</li>
    <li>Sign into GitHub by following the instructions for SSH key authentication. (Note that username/password authentication will NOT work using the command line.) The <code>ssh-keygen</code> tool is available to MacOS, Linux, and <code>git-bash</code> (Windows) users. <a href="https://docs.github.com/en/get-started/quickstart/set-up-git" target="_blank" rel="noopener">https://docs.github.com/en/get-started/quickstart/set-up-git</a>&nbsp;</li>
    <li>See the screencasts at the bottom of this page for setup steps - one is for Mac and one is for Windows.</li>
</ol>

## First-time Configuration

The first time you use git you will encounter a couple of setup issues:

<ul>
    <li>The first time you clone a repository from GitHub using a new ssh key you will get a "key fingerprint" approval request. You can safely say "Yes" to this request, which you will only be asked once.</li>
    <li>The first time you try to commit code on your laptop using git you will be asked to configure two settings - your name and email. This is simply to identify you in the log of commits and changes. Here are the two settings; replace the values in quotes with your own info:</li>
</ul>

    git config --global user.name "Neal Magee"
    git config --global user.email "nem2p@virginia.edu


## WINDOWS USERS

Using `ssh-keygen.exe` in `git-bash` creates a keypair successfully, but (apparently) permissions are incorrect and the normal `chmod 700 keyname` on the private key does not work. This means that git cannot authenticate to GitHub. To resolve this:

<ol style="list-style-type: decimal;">
    <li>Use the <code>ssh-keygen.exe</code> command in git-bash to create a new keypair. Use all the default settings; you do not need to set a password for your key.</li>
    <li>In Windows Explorer, open your <code>.ssh</code> directory and right-click your <code>id_rsa</code> private key. (It may have more numbers and letters added to the name - that's okay.) An easy way to open Windows Explorer in your current directory is: <code>explorer .</code></li>
    <li>Select Properties, then the Security tab and click Edit...</li>
    <li>Check the Deny box next to "Full Control" for all groups EXCEPT Administrators. In my test I only needed to "Deny" full control to the SYSTEM group.</li>
    <li>If you have not already, cat out and copy the contents of your <code>id_rsaXXXX.pub</code> public key to your clipboard. Then visit <a href="https://github.com/settings/keys" target="_blank" rel="noopener">https://github.com/settings/keys </a>and add a New SSH Key. You can name it something convenient and then paste the public key into the "Key" field and save.</li>
    <li>Retry your <code>git</code> commands. You will know it works correctly when you can modify a file, git add it, git commit it, and then git push your changes back to GitHub.</li>
    <li>Watch the screencast at the bottom of the page for how to complete these steps.</li>
</ol>

## Mac

**Here's a walkthrough for Mac users on how to set up git-bash, SSH keys, and GitHub.**

[![Install SSH Keys in Git using a Mac]
(https://i.ytimg.com/vi/rajlGZ3w4OU/maxresdefault.jpg)](https://www.youtube.com/embed/rajlGZ3w4OU?si=UPknm4ygzhenNrRN)


## Windows

**Here's a walkthrough for Windows users on how to set up git-bash, SSH keys, and GitHub.**

<p><iframe title="YouTube video player" src="https://www.youtube.com/embed/X2JgmpkahrY?si=TTvzELmRHoT2jJpM" width="784" height="441" allowfullscreen="allowfullscreen" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"></iframe></p>