# notes
- Pipeline supports combining different type of command . MGET does not .
- MGET and Pipeline uses more memory ,bcz they caches all the response before sending them to client. Pipeline could be better choice bcz it sends the partitional response to client also. 
- Both eliminates the multiple round trips between client and server.
- Also batching happens on redis server's system call to kernal.
