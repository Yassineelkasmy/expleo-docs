# ☕ Configuring Spring boot applications Pipeline with Nexus & GitLab

### First make sure you have the following plugins installed on your Jenkins server:

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

After that we generate an SSH key on the Jenkins server , using the ssh-keygen command, after that we copy the public key and we add it to GitLab

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

Then we go to the Jenkins server command line ( you can use ssh to connect to the archlinux machine ) and we connect to the GitLab server to add it to the known hosts

After this step we have to add the new generated ssh priate key to the Jenkins credentials.

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

Then we go to the system credentials and we click on add credentials.

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

### Create a new multibranch Jenkins job

