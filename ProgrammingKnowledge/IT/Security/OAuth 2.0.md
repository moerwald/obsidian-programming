

> [!note] OAuth is about delegation of access to resources

- Client Application: Appliaktion die Zugriff auf z.B. meine Github Resourcen haben möchte.
- Resource Server: the resources the client wants to get permissions to, in behalf of the user. The resource server can be [twitter](https://www.twitter.com) and the client could be [buffer](https://buffer.com/twitter).

OAuth needs an [[authorization server]] . The client, e.g. [buffer](https://buffer.com/twitter), has to be registered at the [[authorization server]]. During the registration the client receives:

- a client ID
- a client secret
from the authorization server. These credenetials need to be supplied by the client each the client fetches an [[authorization token]] from the authorization server (on behalf of the user).

[From youtube](https://www.youtube.com/watch?v=GyCL8AJUhww)

#### Machine2Machine

![[Pasted image 20230306160556.png]]


#### Human 2 Machine

![[Pasted image 20230306161031.png]]


#### What the user sees

![[Pasted image 20230306161211.png]]

[[Access token]]s are short lived (e.g. 10 minutes). To get a new [[Access token]] the client can you a [[Refresh token]] it received from the [[authorization server]]. The [[Refresh token]] can be valid to weeks or months.

![[Pasted image 20230307084155.png]]
Client View.




![[Pasted image 20230307084520.png]]

User view.


#OAuth2_0