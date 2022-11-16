# CORS-Research


## Dangers of not having Cors enabled
Cors is one of the most important security features in web applications. If Cors is not enabled this will lead
to major security flaws in the application. This is because your application can be called from any domain. We'll dive deeper into this later.

Normally when CORS is enabled your application is secured to only be called from specific domains. 
This is done by setting the Access-Control-Allow-Origin. When this is not correctly done scam sites can be created that will call your application and steal data from it. 

Your application can't see the diffence between a scam site and a real site if Cors is not enabled. This is why a scam site can use the same endpoints as a legit application would be able to use in this case. 

Let's go through an example of how this can be done:

For this example you have a backend application called "TotatllyRealBank" that has a transfer money endpoint.
This endpoint normally is called by a frontend application that is hosted on the domain "TotallyRealBank.com".
The backend endpoint can be called by the frontend application when CORS is not enabled.
Your frontend application would call the backend application with the following request:

```javascript
fetch('https://TotatllyRealBank.com/transferMoney', {
    method: 'POST',
    body: JSON.stringify({
        amount: 100,
        from: '123456789',
        to: '987654321'
    })
})
```
With this request 100 euro will be transfered from account 123456789 to account 987654321.
But a scam site would be able to do the exact same thing. The only thing that would change is the domain name.
The scam site can even modify all the values in the request. Like the amount of money that is transfered or the account the money will be transfered to.

When CORS is disabled your backend will excecute this request and transfer the money to the scam site.

Luckily CORS exists and can be enabled. This will prevent the scam site from calling your backend application.
When correctly setup your own frontend will be able to call this endpoint as usual, but when the scam site tries to call this endpoint you will see you get the following result:
<img src="images/CorsError.png">

Sometimes an Api wishes to be called from any domain. This is possible by setting the Access-Control-Allow-Origin to *. 
This allows everything to call you application. Most of the time this is not a good idea. But for certain GET requests this can be useful. For example when you have a public api that returns data about a certain country. This api can be called from any domain. This is because the data that is returned is public and can be used by anyone.
