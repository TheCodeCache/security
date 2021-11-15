# Digital Certificate #

We need to understand how `digital signature` works, identify its weakness, and that's how we would be able to come to know the need for `Digital Certificate`.  
To know more about `digital signature`, https://github.com/TheCodeCache/security/blob/master/Digital%20Signature.md  

Drwabacks of `Digital Signature`:  
- Lack of Authentication - It does not verify the true identity of the sender and his public key.  

The solution to above the problem:  
`Digital Certificate`:  
  It is an electronic credentials issues by a trusted third party.  
  It not only verified the identity of the owner, but also verifies that the owner owns the public key  

    ![image](https://user-images.githubusercontent.com/26399543/141846124-e320d1a3-7fa7-40e3-91e2-4a0b3c210870.png)

In the above image, the sender sends `digital certificate`, `public key` and the digitaly message.

The Digital Certificate contains:  
1. Certificate's Owner Name
2. Owner's public key and its expiration date
3. The certificate issuer's name
4. The certificate issuer's digital signature
5. Key usage - this hints, whether this is client certificate or server certificate
6. other fields

Sample Example:  

    ![image](https://user-images.githubusercontent.com/26399543/141847599-db69b656-24bc-4088-95c5-b836bf3e4304.png)  ![image](https://user-images.githubusercontent.com/26399543/141847802-7487fc09-8fb0-44be-80bb-7e463f749188.png)  ![image](https://user-images.githubusercontent.com/26399543/141847866-2642ae38-a113-4776-ab9e-dc2c6c979982.png)

The above certificate can be obtained from the green https:// padlock from the browser.  

A `Digital Certificate` is based on `trust` or a `chain of trusts`.  

**Reference:**  
1. https://www.youtube.com/watch?v=UbMlPIgzTxc

