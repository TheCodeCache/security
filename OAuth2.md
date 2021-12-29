# OAuth2 — 

- OAuth2 is an open standard for `access delegation`  
- it stands for `Open Authorization`
- it's **`not`** an authentication protocol, rather a standard to **`delegate access`**
- it's more of a framework,  
an authorization framework than a defined protocol
- it's not for access authentication, it's for access delegation


The delegated authorization problem:  
How can I let a website access my data (w/o giving it my password) ? 

Let's see an example -  
This is a login/signup page from https://www.ishalife.com/in/  

![image](https://user-images.githubusercontent.com/26399543/147697105-a504a3f3-c9a5-4bfc-844a-50325098aa96.png)  

when we click on the google icon to login, below pop-up appears:  

![image](https://user-images.githubusercontent.com/26399543/147697692-9d3a2cf9-32aa-439c-ae31-bf54704e6b10.png)  

there're 2 things to observe from the pop as follows:  

1. >To continue, Google will share your **`name`**, **`email address`**, **`language preference`**, and **`profile picture`** with ishalife.com.

2. >https://**`accounts.google.com/o/oauth2`**/auth/oauthchooseaccount?**`client_id`**=294635701666-ig416g9evmlntlcc7ii1c88os6riafa2.apps.googleusercontent.com&**`redirect_uri`**=https%3A%2F%2Fwww.ishalife.com%2Fin%2Fsociallogin%2Fsocial%2Fcallback%2F%3Fhauth.done%3DGoogle&**`response_type`**=code&**`scope`**=profile%20email&**`access_type`**=offline&**`flowName`**=GeneralOAuthFlow  

once, we select a gmail account and log-in, it logs-in and then google redirect us back to home page of ishalife.com.  
so, we've now logged-into ishalife.com w/o having an account with ishalife website,  
 nor we shared any log-in credential with ishalife website  

All this have been achieved with the support from OAuth2.0 framework.  

OAuth2.0 terminology — 

1. Resource Owner (me / the user who is trying to log-in to ishalife.com)
2. Client (ishalife.com)
3. Authorization Server (accounts.google.com/)
4. Resource Server (contacts.google.come/)  
 - sometimes, the same server can act as Authorization server as well as Resource server both  
5. Authorization Grant (a `token` or a `code` return by Authorization server at step 3 above)
6. Redirect URI (a redirect url, typically client's backend's server, given to Authorization Server)
7. Access Token (ishalife `server` that makes 2nd request to Authorization server  
 to receive the access token by sharing the Authorization Grant received at step 3 above)  


Let us understand its visual workflow and what all are the steps involved in making this happen —  

![image](https://user-images.githubusercontent.com/26399543/147698728-e486f473-d4bf-4745-b88a-26aecdd8cf1d.png)

note:  In the above image, yelp.com/callback url is for the yelp's backend server  

**`scope`** -   
it is the granular resources that the client is asking for -  
for ex: email-id, name, address, location history, profile picture, purchase records etc. any protected details  
the user must review the scopes before login to mail.google.com  

**Query -** Why do we need access token when we already have received the Authorization grant (i.e. token/code) ?   
**explanation -** in n/w-ing, there's 2 channel as follows:  
- back channel (highly secure) for ex: backend server  
- front channel (less secure) for ex: browser  

the problem here is the `auth. grant` can be seen from the browser, may be we can open up the view-source code and check,  
or we can debug the javascript that runs in browser or through the urls query parameter of the address-bar,  
and try to get hold of this `grant` etc.  
so, there's a chance that this grant can go in wrong hand and be misused,  
(all this happens what we call it as `front channel` - less secure)   
that's precisely the reason, the ishalife.com's backend server uses this `grant`  
and asks for the access-token and use this access-token to further access the Resource server,  
(all this happens in what we call as `back channel` - more secure)  

moreover, the exchange of `grant` with `access-token` can only happen in the back channel due to the above security reasons  

usecases (pre-2014) -  
1. simple login (OAuth2.0) - Authentication+Authorization usecase
2. single sign-on access (OAuth2.0) - Authentication+Authorization usecase
3. mobile app login (OAuth2.0) - Authentication+Authorization usecase
4. delegated authorization (OAuth2.0) - Only Authorization usecase

OAuth was never design for the Authentication  
using OAuth for authentication is bad because in OAuth there's no standard way of getting the user's information  
![image](https://user-images.githubusercontent.com/26399543/147700747-8ef8cedd-3a70-46af-b7ce-09cb30928230.png)
solution -  
![image](https://user-images.githubusercontent.com/26399543/147700252-767abd7e-22fd-4c4e-97f1-52c70bc54aa3.png)

OpenID Connect —  
it's not an authentication protocol rather just an extenstion to OAuth2.0  

![image](https://user-images.githubusercontent.com/26399543/147700881-a0b88722-6fb7-4129-b1e4-87e1c8fb6271.png)

The OpenID Connect flow on top of OAuth2.0 —    

![image](https://user-images.githubusercontent.com/26399543/147701157-5c5401e3-cc50-4149-99db-036ab664c0a0.png)


ID-Token is something called JSON Web Token or JWT,  
this JWT is just a standard way of encoding a bunch of information in a way that's easy to transmit over the internet  

![image](https://user-images.githubusercontent.com/26399543/147702065-662b8d1a-fcc6-4d9d-89f8-65e6a3d5bc44.png)

Let us decode the JWT string  

![image](https://user-images.githubusercontent.com/26399543/147702112-1a9c1f3c-17fc-4095-9d43-19e79284acdf.png)



**Reference:**  
1. https://www.youtube.com/watch?v=996OiexHze0

