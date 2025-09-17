# Lab 2

## Team Members
- Ryan Lee ryanhlee1235 ryanhlee@usc.edu

## Lab Question Answers

Question A1: How did the reliability of UDP change when you added 50% loss to your local
environment? Why did this occur?
    The reliability of the UDP went down to receiving around 50-60% of the messages I sent. When I tried the test of sending the sequence of numbers, I was missing the numbers 2, 4, 5, and 10. Because of the 50% loss that was added, not all numbers that sent are going to make it all the way to my server connection. This is because UDP has no method of handling lost or dropped packets, so they essentially just disappear.

Question A2: How did the reliability of TCP change? Why did this occur?
    The TCP reliability didn't change in terms of receiving all the numbers that were sent. However, I did notice that the speed in which the numbers appeared was much slower than when there was no loss. This is because TCP has a system to manage lost packets, like retransmitting a message when a server is missing the receival of expected messages. 

Question A3: How did the speed of the TCP response change? Why might this happen?
    The TCP response speed lowered dramatically. Without the packet loss, it was almost instant, but when the packet loss was added there was a noticeable wait before all of the sequence showed up. This is again because the TCP system has to account for the lost packets in some way, and one of the methods is waiting for acknowledgement that the packets were received. In the inevitable cases that they weren't, the TCP system has to wait until it times out and resend it. This is what leads to the delay in the TCP response.

## tcp_server.c Question Answers:

C1. What is argc and *argv[]?
    argc specifies how many arguments the main function should expect to take, and *argv[] are the input parameters of the actual arguments passed through, including the first argument being the name of the program.

C2. What is a UNIX file descriptor and file descriptor table?
    UNIX file descriptors are integer files assigned to specific files in order to determine a given file's status (specifically if it's open). The file descriptor table is used to create a table of each of these file descriptors and their associated file that they are tracking.

C3. What is a struct? What's the structure of sockaddr_in?
    A struct is like a class in which default access for methods and data are public. The struct defines a blueprint for how an object is created. sockaddr_in takes in members for the address family, port numbers, and an IP address.

C4. What are the input parameters and return value of socket()
    The socket() method takes a couple of parameters. The first one which was AF_INET in this case is the communication domain that is being used. The second parameter is the socket type which was SOCK_STREAM for this code. The third is the protocol, and 0 is the default protocol. The return value of socket() is a non negative integer that is its file descriptor and if it returns -1 that means there was an error.

C5. What are the input parameters of bind() and listen()?
    The input parameters of bind() are the socket file descriptor, then the pointer to the address struct, and then the length of the sockaddr struct. 
    The input parameters of listen() are the socket file descriptor and the max number of pending connections for the socket. 

C6.  Why use while(1)? Based on the code below, what problems might occur if there are multiple simultaneous connections to handle?
    The while(1) means that the program will run indefinitely as long as there are no errors. This is used because the server is always waiting and listening for a client message to be sent.
    Since the code seems to only be accepting one socket and address, this means that the code is not programmed to be able to take multiple connection requests at once, especially now that it is stuck in this infinite while loop, it has to be responsible for handling the client interaction.

C7. Research how the command fork() works. How can it be applied here to better handle multiple connections?
    The fork() command allows a process to be split up into a parent process and a child process. The child process can handle the existing client interactions, while leaving space open for the parent process to continue accepting new connections.

C8. This program makes several system calls such as 'bind', and 'listen.' What exactly is a system call?
    A system call is a request that the program makes to the operating system's kernel. For example, the OS kernel handles the underlying infrastructure for sockets, but each language has an implementation for it.


Question A4: If you used LLMs for any part of this lab, explain how you used it
    I did not use LLMs to help me with any of the coding portions. However, I used the Google AI overview alongside other websites and sources to help with my understanding for the subjects that the questions were on.