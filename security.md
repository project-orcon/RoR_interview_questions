#Security Questions

####Explain what is a sessions mechanism. How does it work?
HTTP is a stateless protocol (no way of telling which user made which request as it doesn’t store state). Sessions make it stateful. A session is just a place to store data from one request that can be read from other requests. You generally don’t want to store data in a cookie as they can only store 4kb of data, and they are sent with every website request made, which means larger cookies lead to longer response times - however you can using cookieStore. A better idea is storing sessions data using activeRecord. Rails stores the session ID in the cookie, and the relevant data in the sessions table. The ID is later read from the cookie and used to fetch this data. Besides storing data in cookies and the database you can also store the data in cache, using something like Memcache. Storing in cache means it is faster (kept in memory) and older sessions will immediately be kicked out if it gets too big. However sessions and cached data will be fighting for space, if you don’t have enough memory you could be getting early expired sessions. By default rails uses cookieStorage for the session. 

####Describe cross-site request forgery, cross-site scripting, session hijacking, and session fixation attacks.

Cross-site request forgery(CSRF) involves the attacker embedding urls in pages/emails to sites which the user may be logged into. They can make post requests to delete items in the users account for example. CSRF is protected against by adding CSRF tokens to each post request so that only the webpage itself can be used to send a post request.

Cross site scripting attacks involve, the attacker being able to run code on the target site. Such code is normally embedded javascript that is inserted via text box (in the comments page on a site for example). The code can access the users session_id and send it to the attackers own site. Enabling the attacker to steal the users session.

Session Hijacking involves stealing the users session data. This can be done by the user having physical access to the computer and copying the cookie or by data sniffing on an unsecured network. In order to prevent the latter its important that all requests are to the website are made via HTTPS. 

Session Fixation involves the attacker forcing the user to use their own session id. It involves the attacker going to the login page of the site and retrieving the session_id (not logged on yet), or generating a session_id that’s in the correct format. Then using XSS or other means the attacker gets the user to set their session_id to the attacker’s. When the user then authenticates the attacker is also able to access their session too. Session fixation can be prevented by creating a new session once the user successfully authenticates (this is a rails default).

####What is the difference between SQL Injection and CSS Injection?

CSS injection involves the attacker inserting their own CSS into a vulnerable site. It can potentially be used to read form data or anti CSRF tokens thus allowing a CSRF attack. It is similar to XSS except css rather than javascript is used. It uses the CSS attribute selectors in conjunction with background URL to enable the attacker to log values. 
SQL injection involves a user running SQL queries that are not supposed to be run. Typically by inserting values which cause the existing query to be terminated, and instead running another attack query. In order to prevent this queries must be parameterised. Basically if you ever see a active record function that contains a single quote within double quotes, or a interpolated string it is most likely vulnerable to SQL injection. For example this line is vulnerable.

@writers = @writers.where("biography like '%#{params[:query]}%’")

however this line is not. 

@writers = @writers.where("biography like ", params[:query])

this line is vulnerable

User.where("email = #{payload}").first


####How should you store secure data such as a password?

Secure data such as a password should be encrypted and stored in a one way hash. and stored in the database. To store secret keys for accessing apis you should use environmental variables. However there are other ways too https://blog.arkency.com/2017/07/how-to-safely-store-api-keys-in-rails-apps/.

####Why do we need to use HTTPS instead of HTTP?

To make sure all data sent between the client and server is encrypted via SSL. This prevents any network sniffers from accessing any data sent between the two, potentially stealing a users login details or session id. It also prevents users from falling victim to man in the middle attacks, if using Extended Validation SSL. 