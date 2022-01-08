User Moderation
=================

The User based moderation is done through the following Smart Contract: `KT1TWWQ6FtLoosVfZgTKV2q68TMZaENhGm54`.

# How to moderate

The entry-point `moderate` of the contract needs to be called. Only accounts added as **moderators** to the contract can call the entry point.

It takes 2 parameters:

* 0: the **tz address** of the account to moderate
* 1: an **integer** representing the state to associate with the user

The following states are available (sending the integer to the `moderate` entry point will assign the associated state to the user account):

* **0**: `NONE` - default state for the users
* **1**: `REVIEW` - account is under review, a Flag will appear on their profile. It does not affect the Generative Tokens they could post.
* **2**: `SUSPICIOUS` - account clearly shows some suspicious behaviour, be it cannot be classified as `MALICIOUS` with enough certainty. It does not affect the Generative Tokens they could post.
* **3**: `MALICIOUS` - account clealy shows some malicious behaviour, and it can be proven. Users flagged as `MALICIOUS` will have all of their Generative Tokens posted **after** moderation flagged as `MALICIOUS`. Already posted Generative Tokens must be flagged manually individually.
* **10**: `VERIFIED` - user was verified by the moderation team


## Shorcuts

The new contract exposes 2 entry points to **ban** and **moderate** users:

* verify(address) -> moderate(address, 10)
* ban(address) -> moderate(address, 3)


# Side-effects of moderation

When the `moderate` entry point is called, it will associate a Flag to a tezos address. The account will then be flagged on its profile with a message corresponding to the flag associated with them. By default, Users have a flag set to `NONE`. Users with a flag set to `NONE` don't have a flag banner on their profile. Setting the flag to `NONE` through the contract will reset user's flag to their default value, and will make the banner disappear if any.

If the flag of a user is set to `MALICIOUS`, then any Generative Token they will post will automatically flagged as `MALICIOUS`. As a result, it will be hidden from the front-end and have the appropriate banner associated with it if someone were to load its page.

This contract exposes on-chain views to get a user's state, and so it's possible for other contract to get the state of the sender and block certain actions if required. For instance, if a user is banned, they won't be able to call the `mint_issuer` entry point and so they won't be able to publish new Generative Tokens.