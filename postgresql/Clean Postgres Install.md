#postgresql 
```bash
# Follow the commands:

sudo apt-get --purge remove postgresql
# List all postgres related packages:

dpkg -l | grep postgres
remove all the above listed packages using the command :

apt-get --purge remove package1 package2 ..
# Confirm all the files and folders related to postgres/postgresql are deleted using the command :

whereis postgres
whereis postgresql
# Remove all the files and folders listed using rm command.

# Delete the user postgres using the command :

userdel -f postgres
```