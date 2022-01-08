Generative Token Moderation
=================

The Token moderation is done through the following Smart Contract: `KT1BQqRn7u4p1Z1nkRsGEGp8Pc92ftVFqNMg`.

# How to moderate

The entry-point `moderate` of the contract needs to be called. Only accounts added as **moderators** to the contract can call the entry point.

It takes 2 parameters:

* 0: the **id** of the Generative Token to moderate
* 1: an **integer** representing the state to associate with the token

The following states are available (sending the integer to the `moderate` entry point will assign the associated state to the user account):

NONE              = "NONE",
CLEAN             = "CLEAN",
REPORTED          = "REPORTED",
AUTO_DETECT_COPY  = "AUTO_DETECT_COPY",
MALICIOUS         = "MALICIOUS",
HIDDEN            = "HIDDEN",

* **0**: `NONE` - default state for the tokens
* **1**: `CLEAN` - token was inspected and it's definitely clean. Generative Tokens set as CLEAN have their reports ignored.
* **2**: `REPORTED` - token was reported because it's suspicious, but it's not been stated yet if it MALICIOUS. This state is different from users reporting the token.
* **3**: `MALICIOUS` - Generative Token shows some malicious behaviour, and it can be proven. Generative Tokens flagged as `MALICIOUS` will have all of their Generative Tokens posted **after** moderation flagged as `MALICIOUS`. Already posted Generative Tokens must be flagged manually individually.