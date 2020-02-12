- By default
  - the echo command takes the input (standard input or stdin) from the keyboard
  - and returns the output (standard output or stdout) to the screen.

- However, I/O redirection allows us to change this default behavior giving us greater file flexibility.

- redirection operator
  - > : overwrite the file
  - >> : append to the end if the file exists

- we have different stdout streams we can use, such as
  - a file
  - the screen

- We know that we have stdin from
  - devices like the keyboard
  - but we can use files
  - output from other processes
  - and the terminal as well

- Just like we had > for stdout redirection, we can use < for stdin redirection.

- Normally in the cat command, you send a file to it and that file becomes the stdin

- By default, stderr sends its output to the screen as well, it's a completely different stream than stdout.

- Unfortunately the redirector is not as nice as using < or > but it's pretty close.
  - We will have to use file descriptors.
  - A file descriptor is a non-negative number that is used to access a file or stream.

- the file descriptor for stdin, stdout and stderr is 0, 1, and 2 respectively.

- The pipe operator |, represented by a vertical bar, allows us to get the stdout of a command and make that the stdin to another process.

- Well what if I wanted to write the output of my command to two different streams? That's possible with the tee command

- cut, paste, head, tail
