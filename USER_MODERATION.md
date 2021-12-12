User Moderation
=================

The User based moderation is done through the following Smart Contract: `KT1CgsLyNpqFtNw3wdfGasQYZYfgsWSMJfGo`.

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


# Side-effects of moderation

When the `moderate` entry point is called, it will associate a Flag to a tezos address. The account will then be flagged on its profile with a message corresponding to the flag associated with them. By default, Users have a flag set to `NONE`. Users with a flag set to `NONE` don't have a flag banner on their profile. Setting the flag to `NONE` through the contract will reset user's flag to their default value, and will make the banner disappear if any.

If the flag of a user is set to `MALICIOUS`, then any Generative Token they will post will automatically flagged as `MALICIOUS`. As a result, it will be hidden from the front-end and have the appropriate banner associated with it if someone were to load its page.