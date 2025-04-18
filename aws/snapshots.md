# SNAPSHOTS
- SNAPSHOTS in aws help us to take point-in-time back up for ebs volume.
- Snaphots works in incremental way, means that during first snapshot entire volume state backup & next subsequent snapshots will capture only the delta changes on volumes from previous snapshots.
- Incremental snaphots will increase speed & save storage.

# TASK1: 
- Create webserver1 instance, attach EBS volume & later store date in that volume.
- Then take snapshot of EBS volume,create volume out of snapshot & attach to webserver2. 
- Here we have to see the data that we created in webserver1

- Create t2.micro instance of name webserver-1
- Create volume in same AZ where webserver-1 created.
- Attach volume to the EC2
- Check disk detected or not in machine
    lsblk
- Setup filesystem to make operating system to store files on disk
    mkfs.ext4 /dev/xvdf
- Mount the volume
    mkdir /ebsvol/webserver1
    mount /dev/xvdf /ebsvol/webserver1
- Create folders & files
    cd /ebsvol/webserver1
    mkdir folder1 folder2
    echo "this file is in folder1" > file1.out
    echo "this file is in folder2" > file2.out
- Take snapshot of volume
- Create volume of snaphot & we can't reduce the size of volume
- Attach volume to webserver-2
- check disk detected or not in webserver-2
- Mount volume
    mkdir /ebsvoltest
    mount /dev/xvdb /ebsvoltest
- Now we can see the files in webserver-2 that we have taken backup.


# TASK2: Share the snapshot within same region to another account
- Snapshots ==> Choose snapshot ==> Actions ==> Snapshot settings ==> Modify Permissions
- Public: Make it accessible to all user
  Private: Make it accssible to specific account.

# Task3: Share the snapshot to other region in same account
    - Snapshots ==> Choose snapshot ==> Actions ==> Copy snapshot
    - Choose destination region that you want to copy

# Life cycle Manager
- Using this option we define a policy 
    - For which ebs volumes snapshots hase to be taken based on tags
    - scheduling timings for taking snapshots
    - purging the old backups


# PENDING
- How automated snapshots will be taken
- How to set retention policy
- How to setup encryptio
