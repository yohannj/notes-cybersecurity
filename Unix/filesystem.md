# Unix important files
/etc/passwd					# User infos
/etc/shadow					# User passwords
/etc/sudoers				# Control who can sudo
/etc/issue					# Msg printed before login prompt
/etc/profile				# Default variables
/proc/version				# Linux kernel version
/tmp 						# Temporary files
/root						# Root home directory
/root/.bash_history			# Command history of root
/usr						# Software
/bin /sbin					# Critical files
/var						# Linux misc directory
/var/log/dmessage			# Global system messages
/var/mail/root				# root emails
/var/log/apache2/access.log	# Accessed requests for Apache webserver
/root/.ssh/id_rsa			# root private ssh key
$PATH						# Binaries I can run
/etc/crontab				# Crontabs

# SUID
Files with the SUID bit set can be run with the permissions of the files owner/group.
This can be used to do priviledge escalation.
