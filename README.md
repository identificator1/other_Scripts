# Backup Jenkins Server via ssh (scp with ssh key) for macOS (or Linux) servers

M - Master (source) Jenkins Server
D - destination server for backup

1. Generate keypair (or use existing) on M: ssh-keygen (default public: ~/.ssh/id_rsa)
2. copy the public key to D: ssh-copy-id user_on_D@ip_or_DNS_of_D
3. check an access: ssh user_on_D@ip_or_DNS_of_D
4. create a folder on D server: /backup with proper permissions
5. create a schedule: crontab -e (run sudo touch /etc/crontab if doesn't allow from the first time): * 2 1-31/7 * * tar -cvzf ~/weeklybackupjenkins.tar.gz --exclude='jobs/*/builds' -C /jenkinshomefolder . # every 7nd day at 2:00AM
6. and * 3 1-31/7 * * scp -i ~/.ssh/id_rsa ~/weeklybackupjenkins.tar.gz user_on_D@ip_or_DNS_of_D:/backup # every 7nd day at 3:00AM
