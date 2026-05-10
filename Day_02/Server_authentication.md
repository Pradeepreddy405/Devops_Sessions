SSH key authentication is based on asymmetric cryptography and is commonly used in Linux and cloud environments for secure remote access.

When we execute `ssh-keygen` on the client machine, it generates a key pair:

* A private key, which stays securely on the client system
* A public key, which is copied to the target server inside the `~/.ssh/authorized_keys` file

During the SSH connection process, the server checks whether the client possesses the correct private key corresponding to the stored public key.

The important part is that the private key is never transmitted over the network.

Instead, the SSH server generates a cryptographic challenge. The client signs that challenge using its private key, and the server validates the signature using the stored public key. If verification succeeds, access is granted.

This is significantly more secure than password authentication because:

* There is no password transmission
* Brute-force attacks become extremely difficult
* Keys are mathematically linked and computationally hard to crack
* It supports secure automation in DevOps environments

In real-world infrastructure, SSH keys are widely used for:

* EC2 instance access in AWS
* GitHub and GitLab authentication
* Jenkins deployment pipelines
* Ansible automation
* Terraform provisioning
* Secure server-to-server communication

From a security perspective, production environments usually:

* Disable password authentication
* Use passphrase-protected private keys
* Enforce strict file permissions
* Rotate keys periodically
* Use bastion hosts or centralized access management

This approach provides both strong security and operational efficiency for large-scale infrastructure management.
