- /etc/passwd - shows you a list of users and detailed information about them
- /etc/shadow - store information about user authentication
- /etc/group  - allows for different groups with different permissions

- User Management Tools:
  - useradd
  - userdel
  - passwd

- chmod/chown/chgrp

- umask

- SUID/SGID - when a file has this permission set, it allows the users who launched the program to get the file owner's permission as well as execution permission

- effective user ID, real user ID, saved user ID

- permissions:
  - r - read
  - w - write
  - x - execute
  - s - The Set User ID (SUID), 取代 x 那個字元
  - t - The Sticky Bit, 最後一個字元
