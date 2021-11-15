# Digital Signature #

A `digital signature` is equivalent to a handwritten signature.  
It is an electronic verification of the sender.  

It serves 3 purposes as follows:  
1. `Authentication` - it servers as the authentication of the claimed sender.
2. `Non-repudiation` - the sender can not deny having sent the message later on.
3. `Integrity` - it ensures that the message was not altered during transit.

It is commonly used for software distribution, financial transactions.  
it has been also popular with email users.  

It uses `Asymmetric Key Cryptography`.  

    ![digital_signature](https://user-images.githubusercontent.com/26399543/141843072-9e5b48a9-e770-400e-b500-85680feb84fd.png)

Note: Digital Signature `does not encrypt` the message itself.  

Drawback:  
  It is prone to attack, any one can pretend being a fake sender, and thus, the real data could be compromized.  

Reference:  
1. https://www.youtube.com/watch?v=TmA2QWSLSPg&t=17s

