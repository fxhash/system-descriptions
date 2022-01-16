The cycles implementation
=============

Cycles are implemented directly in the contracts, and access to certain features limited by the cycles are limited per contract rules.
A generic-purpose cycles contract defines a list of cycles which can be used by any other contract if needed:

* Cycles contract: `KT1ELEyZuzGXYafD2Gar6iegZN1YdQR3n3f5`

The contract stores a list of cycles, each cycle is defined as following:
* `start time` (timestamp): a time reference for when the cycle starts
* `opening duration` (seconds): the duration for which the cycle will be opened
* `closing duration` (seconds): the duration for which the cycle will be closed

This is the lifecycle of a cycle:

`START TIME` -> `OPENING TIME` -> `CLOSING TIME` -> `OPENING TIME` -> `CLOSING TIME` -> ...

The cycles contract implements on-chain views to help other contracts get informations on the state of a cycle(s) given a certain time.

* `is_cycle_opened(cycle_id, timestamp)`: returns true if the cycle identified by `cycle_id` is opened at the given `timestamp`
* `are_cycles_opened(cycle_ids, timestamp)`: returns the AND operation between the results of `is_cycle_opened` applied on all the cycles identified by `cycle_ids`

Basically, cycles will be opened at a certain time if and only if all the cycles are opened.