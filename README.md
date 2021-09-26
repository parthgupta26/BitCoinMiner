# COP5615 Distributed Operating System Principles Project 1

## Bitcoin-Miner-Actor-Model-F#-Akka.Net

## Project Description

Generate a random string with an initial string as your gator Id and find the hash of that string with k leading 0's provided by the user in the command line.

## Project Requirements

### Input

The input provided (as command line to yourproject1.fsx) will be, the required number of 0’s of the bitcoin.

### Output

Print, on independent entry lines, the input string, and the corresponding SHA256 hash separated by a TAB, for each of the bitcoins you find. Obviously, your SHA256 hash must have the required number of leading 0s (k= 3 means3 0’s in the hash notation).  An extra requirement, to ensure every group finds different coins, is to have the input string prefixed by the gator link ID of one of the team members.

### Example:

dotnet fsi yourproject1.fsx 1 <br>
adobra;kjsdfk11    0d402337f95d018438aad6c7dd75ad6e9239d6060444a7a6b26299b261aa9a8b

## 1

The project aims to print all the possible bitcoins after mining with k leading zeros, but for the purpose of printing only one answer I have declared one varialble named coinCount which can be updated to 1 from 0 whenever we got the first result, on line number 127 of AkkaServerMiner.fsx. This is done in order to print only single output for some value of k. Program is run as follows:
- k is some integer >= 0
- dotnet fsi AkkaServerMiner.fsx k
- After the cosole shows that server is trying establishisng a connection we run AkkaRemoteMiner.fsx as:
- dotnet fsi AkkaRemoteMiner.fsx

### Server Side

- The project consists of two files first AkkaServerMiner.fsx and second AkkaRemoteMiner.fsx. Initially a server starts while creating a remote configuration port, where the other actors that is from client can connect too.
- Server then itself stars with two actors at server side (assuming two cores of the physical machine) and server will now have two working actors.
- The echoServer function in the AkkaServerMiner.fsx receives the metadat such as number of zeros required to create a hash, the initial string that is gator ID, and the allocated length.
- Now the boss system is created inside the echoServer who recursively calls a loop to receive output from various actors (including client side as well).
- The message received from these actors is now matched with the type of output that is expected and the action is taken according to the validity of the answer. For example [Answer, ComputationalMetaData, and string message from actors].
- When a signal is received from an actor it sends back a response to the sender actor to start working with a given length again, it meant it starts working with some allocated length.
- Now the actor hashActor_worker calls the findSha256for method along with serverSideActor reference. After this when a hash is computed for many random strings and matched with the requirement of k leading zeros (this is achieved by calling checkKLeadingZeros method). If we get the required answer the correct response is sent back to the server as answer and the answer is printed with a tab and then a hash of that string.

### Remote Side

- Now this AkkaRemoteMiner.fsx will be connected to remote server created by AkkaServerMiner.fsx on the port number configured that is 5000. The remote file will create 6 more actors and then start the same hash computation for random strings using a recursive loop.
- Whenever a match is found with required number of zeros, it sends a response back to the server, that result has been found (matched = str).

## 2

The result of running of my program for input 4 (Some part of the output).

parthgupta !dH    0000aad243ce6b9dedbae92e2c0f3f9cbdb13477931328a5431771f72e0b5893 <br>
parthgupta '&A    0000933f99470974706b0c1f1f9e8f0806fa1bb72183bf7a7dc2dd5a46adf5f8 <br>
parthgupta 1)#    00002377d9c1b058c296f63013798466d7c053a994d3792afa4158f0a2dd4688 <br>
parthgupta 6 E    0000bdc1ff21194496cc0f17feef04d58e047e110b63c5e0894093c9dc6955eb <br>
parthgupta8xH    000085d5d086abd6798cdfd18045f3dc312dd1ac47ae23bf9065e7f0ed0676dc

The result of my program when I printed only single answer and exits the program.

PS C:\Users\Parth Gupta\desktop> dotnet fsi AkkaServerMiner.fsx 4 <br>
Real: 00:00:00.000, CPU: 00:00:00.000, GC gen0: 0, gen1: 0, gen2: 0 <br>
[INFO][25-09-2021 00:10:21][Thread 0001][remoting (akka://AkkaRemote)] Starting remoting <br>
[INFO][25-09-2021 00:10:22][Thread 0001][remoting (akka://AkkaRemote)] Remoting started; listening on addresses : [akka.tcp://AkkaRemote@127.0.0.1:5000] <br>
[INFO][25-09-2021 00:10:22][Thread 0001][remoting (akka://AkkaRemote)] Remoting now listens on addresses: [akka.tcp://AkkaRemote@127.0.0.1:5000] <br>
parthgupta !dH    0000aad243ce6b9dedbae92e2c0f3f9cbdb13477931328a5431771f72e0b5893 <br>
Real: 00:00:02.352, CPU: 00:00:04.671, GC gen0: 595, gen1: 3, gen2: 0 <br>
PS C:\Users\Parth Gupta\desktop>

## 3

The running time for the above as reported by time for the above and report the time.

Real: 00:00:02.352, CPU: 00:00:04.671, GC gen0: 595, gen1: 3, gen2: 0

RATIO of CPU TIME to REAL TIME = (4671/2352) = 2 (Approximately). [Taking time in milliseconds]

## 4

The coin with the most 0s I was managed to find was for k = 7.

parthgupta 5AhU    00000006ad1c1c530aa6de7a361ecb04ea048aaa6c1359f616ed6041dbfad880 <br>
parthgupta:KeP    000000054d9839816bd6a3f5123ca761d33cb0520b54a10323223822fd859c98

## 5

The largest number of working machines on which I was able to run my code = 1 (My System).

## Built On
- Programming language: F# 
- Framework: AKKA.NET
- Operating System: Windows 10
- Programming Tool: Visual Studio Code
