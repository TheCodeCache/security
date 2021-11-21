Generic answer : **Depends on the use case.**

`Server side encryption` from aws is almost free or very cheap.  
  Managing `key` and `encryption` every thing is taken care by AWS.  
  When we upload an object to S3 plaintext is visible to aws.  
  It will encrypt it and whenever needed, it will `decrypt` the content with the key.  
  AWS has access to encryption key.   

`Client side encryption`: we will manage everything.  
  `Key`, `encryption` or `decryption` will all be taken care by us.  
  It will cost us, but AWS will only see ciphertext.  

So, when we `trust` AWS with our data and keys and `cost is a consideration` we go with Server side.  
  But when we've our own encryption infrastructure,   
  and, we've specific requirements (encryption other than AES-256 etc.) we should choose for client side.  

# Important Note:  
Technically, **over HTTPS**, any data sent is subject to **client-side encryption**
  
  
  
  
**Reference:**  
- Quora
- https://qr.ae/pGmOFj

