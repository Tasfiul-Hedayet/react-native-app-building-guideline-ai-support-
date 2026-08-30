# How to avoid hardcoded credentials in react native app 
(bcuz if we keep .env file inside the app, attacker
can decompile and see the hardcoded credentials)

## instead of using supabase directly on react native app, there are 2 ways. 

* Proxy server (using express.    backend)
* Supabase edge functions 


How supabase edge functions works?

