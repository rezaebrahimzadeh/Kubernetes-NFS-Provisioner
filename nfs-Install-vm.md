# Setting Up NFS in Ubuntu VM

Network File Share (NFS) is a protocol used for sharing files and directories over a network. Essentially, a shared directory is created, and files are added to it so that clients can easily access them. Using NFS is also ideal when you need to exchange common data between different client systems.

## Installation Steps

1. **Install NFS on Ubuntu VM**:
   - Run the following command in the Ubuntu terminal to install the NFS server:
     ```
     sudo apt install nfs-kernel-server
     ```

2. **Create an NFS Shared Directory**:
   - Choose a path (e.g., `/mnt/nfs`) for your shared directory:
     ```
     sudo mkdir -p /mnt/nfs
     ```

3. **Set Permissions for the Created Directory**:
   - Ensure that all client machines can access the "nfs" directory:
     ```
     sudo chown -R nobody:nogroup /mnt/nfs/
     ```

4. **Adjust File Permissions**:
   - In our example, we've assigned read, write, and execute permissions to files in the "nfs" directory. Adjust access according to your organization's policy:
     ```
     sudo chmod 777 /mnt/nfs/
     ```

5. **Configure Access for Client Systems**:
   - Open `/etc/exports` using the `vim` or `nano` editor and set access permissions:

   ```plaintext
   # /etc/exports: the access control list for filesystems which may be exported
   #               to NFS clients. See exports(5).
   #
   # Example for NFSv2 and NFSv3:
   # /srv/homes       hostname1(rw,sync,no_subtree_check) hostname2(ro,sync,no_subtree_check)
   #
   # Example for NFSv4:
   # /srv/nfs4        gss/krb5i(rw,sync,fsid=0,crossmnt,no_subtree_check)
   # /srv/nfs4/homes  gss/krb5i(rw,sync,no_subtree_check)
   /mnt/nfs 192.168.8.0/24(rw,sync,no_subtree_check)


Customize the IP range (e.g., 192.168.8.0/24) to match your network configuration.

```
sudo systemctl restart nfs-kernel-server

```
