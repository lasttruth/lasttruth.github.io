---
layout: post
title:      "Bcrypt and the has_secure_password method"
date:       2018-09-09 22:36:49 -0400
permalink:  bcrypt_and_the_has_secure_password_method
---


Hello Today,


Today I want to light an important matter when it comes to protecting information of potential users. That is the bcrypt and `has_secure_password `. You may be wondering "what is bcrypt and what can it do for my website!?" well I'm glad you asked. It starts off like this.



**WHAT IS BCRYPT!?**



Bcrypt is a hashing algorithm that encodes an end user's password. Think about this technology changes fast. Increasing the speed and power of computers can benefit both the engineers trying to build software systems and the attackers trying to exploit them. Meaning that the stronger the hardware the faster a hacker can decode a password. To minigate this we need a hashing algorithm that slows down that process.  How? Bycrpt take a chunk of data *ahem* your Password for your Facebook and creates a "digital fingerprint" or a hash and adds salt to it. Im not kidding when I learned about this I came with Salt and Pepper, with pepper being the password.  So think of this

```
Hash (InsErtComPlicateDPasSWord + salt) = <gibberish that only a computer can understand>
```

You might be wondering what is Salt? Salt is is just random data added to the password before it's hashed. Where does the random data comes from? I personally do not know but I think thats the point. Plus this process is not reverisble so there's no for an attacker can go from hash to password. (Yep I can smell the steam coming from an hacker's brain.) After your Salt and Pepper gribberish is created, it is stored and used to check potentially valid passwords

```
<Gibberish only a computer can love> =? hash(salt + insert_recently_created_password)
```

Now you're COOKING. (get it?... No?...k.)

With is encryption it becomes hard to crack your password, making you safe. It still never hurt to have two step verification just to have a clear mind in the long run. 

**has_secure Password**

Along with Bcrypt we need a handy macro called has_secure_password and an attribute called password_digest.
Together we have a way that doesn't store the plain text password in the database. This ActiveRecord macro gives us access to a few new methods. A macro is a method that when called, creates methods for you. (Meta programing is awesome.) Since these fields aren't connected to database columns, the method expects there to be a password_digest column defined in your migrations. Has_secure_password also adds some before_save method to your model. These compare password and password_confirmation. We also need to check if that user's password matches up with the value in password_digest. Users must have both an account and know the password.
We validate password match by using a method called `authenticate` on our User model. We do not have write this method ourselves. (META!!) Let's explore `authenticate` a bit, it takes a String as an argument like `toyRus_RIP`  and turns its into a salted, hashed version `76776516e058d2bf187213df6917a7e`. Now the method compares this hashed version with the one thats is stored. If the two verions match, `authenticate` will return the User instance. if not, it returns false. If it does return false you can redirect the user to the login page with an error message saying "ACCESS DENIED".
