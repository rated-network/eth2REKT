# eth2REKT

eth2REKT is a twitter bot that tracks slashing events on the eth2 network. The bot also happens to be an homage to the legendary game and movie series Mortal Kombat. 

## How to read the tweets

eth2REKT’s tweets follow the following convention:
```
Validator [val_id] {id_tag | character | eth_wealth | abbr_depo_address} 
was slashed by 
validator [val_id] {id_tag | character | eth_wealth | abbr_depo_address | slasher_pedigree}

Condition: [condition]
Slot: [slot] 
Slash streak: [streak]

~ [MK_one_liner]
```
Below you will find an explainer on what each of the variable fields (in brackets `[…]` above) represent: 

* `val_id`: this is the validator index of the slashed validator and the proposer/whistleblower that included the slashing proof equivalently
* `id_tag`: this is an approximation the identity behind said validator index. We approximate that using data from nansen.ai on the deposit address associated with said validator index
* `character`: this is a heuristic on the type of activity this address has been involved in historically. We use data from nansen.ai and duneanalytics.com to qualify that
* `eth_wealth`: this is a heuristic that points to the footprint of said address on the eth2 network (% ownerhsip). We provide with a table of classification below
* `abbr_depo_address`: this is the abbreviated (5 first digits) deposit address associated with said validator index
* `slasher_pedigree`: this is a label that signifies the amount of slashes that the eth_address associated with said validator index has enforced over its history of activity on the the eth2 network
* `condition`: this qualifies the condition that underlies each slashing event. We qualify between “Double Prooposal” for proposer violations,  and “Double Vote” and “Surround Vote” for attestation related violations. 
* `slot`: the slot that the slashes were included in
* `streak`: the number of consecutive slashes a specific eth1_deposit_address has been subject to (note: this will represent multiple validator indices)
* `MK_one_liner`: a series of Mortal Kombat one-liners taken directly from MK’s lore, because life is too short to take yourself too seriously. While these will be randomly generated for unrelated addresses being slashed, once the slash streak counter starts rising, they start following a different pattern to communicate the escalating situation. We explore the logic below.

On days when no slashings take place, the bot will update on how many days have gone by without a slashing even recorded on eth2.

## Slasher predigree naming conventions

The following naming conventions describe the amount of slashings that each of the eth1 deposit addresses has enforced, via their related validators (expressed as val_ids).
|Slashings |Tag          |
|----------|-------------|
|1-5       |Noob Saibot  |
|6-10      |Reptile      |
|11-15     |Sub Zero     |
|15-20     |Scorpion     |
|20-30     |Prince Goro  |
|30-50     |Shang Tsung  |
|50+       |Shao Khan    |

## Slash streak naming conventions

To convey the rising intensity in a particular operator getting slashed multiple times and call out attention to the magnitude of the event, we have decided upon the following formatting conventions, for a rising slash streak count.
| Slash streak | Tag               | Emojis                       |
|--------------|-------------------|------------------------------|
| 1            | random one-liner  | random emoji                 |
| 2            | Toasty!           | 🔥🔥                          |
| 3            | Finish him!       | 🩸🩸🩸                   |
| 4            | Friendship        | 🌼🌱🎊🧸                  |
| 5            | Babality          | 👶🏻👶🏼👶🏽👶🏾👶🏿        |
| 6            | BRUTALITY!        | 👹👹👹👹👹👹              |
| 7            | FATALITY!         | ☠️☠️☠️☠️☠️☠️☠️ |
| 8            | STAGE FATALITY!   | 🩸🩸🩸🩸🩸🩸🩸🩸    |
| 9            | ANIMALITY!        | 🦙🐅🦑🐘🐍🐒🐁🐆                  |
| 10+           | Flawless victory! | 💯💯💯💯💯💯💯💯💯💯        |
