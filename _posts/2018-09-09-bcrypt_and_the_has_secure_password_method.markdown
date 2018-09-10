---
layout: post
title:      "Bcrypt and the has_secure_password method"
date:       2018-09-09 22:36:49 -0400
permalink:  bcrypt_and_the_has_secure_password_method
---


Hello Today,


Today I want to light an important matter when it comes to protecting information of potential users. That is the bcrypt and `has_secure_password `. You may be wondering "what is bcrypt and what can it do for my website!?" well I'm glad you asked. It starts off like this.



**WHAT IS BCRYPT!?**



Bcrypt is a hashing algorithm that encodes an end user's password. Lets role play for a bit, I will play the hacker and you will be the unsuspecting Facebook user. In this scenario lets say Facebook doesn't have way to encrypt password well. Okay one day you walk into Starbucks to get a nice cup of coffee on your lunch break and decided to check Facebook for a bit. Me as the hacker is sitting on the other side of store with my hacking program ready to go notice you're connected to store WiFi and is on Facebook. After a few moments I manage to pull up your information that I can use to login to your account and take your identity on Facebook. After inspecting the data I just gathered I found out that your password is...

"CatsAreBetterThanDogs3000"

Well whereas that statement is highly concerning seeing as dog are better( Yeah i went there.)  There is something far more concerning. Your password is in plain text. This is bad for you and three times as bad for the folks at Facebook. If everyone's password is easily accessible then it will cause problem and potentially ruins people lives. 

This is where bcrypt comes in.  Bcrypt encrypt your password into random assortment of characters something like this
```
$2b$10$69SrwAoAUNC5F.gtLEvrNON6VQ5EX89vNqLEqU655Oy9PeT/HRM/a
```


With is encryption it becomes hard to crack your password, making you safe. It still never hurt to have two step verification just to have a clear mind in the long run. 

**has_secure Password**

Along with Bcrypt come a handy method called has_secure_password and an attribute called password_digest.
Has_secure_password adds method to set and authenticate against a BCrypt password. Has_secure_password adds two fields to your model: password and password_confirmation. Since these fields aren't connected to database columns, the method expects there to be a password_digest column defined in your migrations. Has_secure_password also adds some before_save method to your model. These compare password and password_confirmation. If they match then it updates the password_digest. These fields are designed to make it easy to include a password confirmation box when creating or updating a user.

