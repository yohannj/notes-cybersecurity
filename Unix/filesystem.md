# Unix important files
/etc/passwd		# User infos
/etc/shadow		# User passwords
/tmp 			# Temporary files
/etc/sudoers	# Control who can sudo
/root			# Root home directory
/usr			# Software
/bin /sbin		# Critical files
/var			# Linux misc directory
$PATH			# Binaries I can run

# SUID
Files with the SUID bit set car be run with the permissions of the files owner/group.
This can be used to do priviledge escalation.