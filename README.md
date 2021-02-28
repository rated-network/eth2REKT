# eth2REKT

eth2REKT is a twitter bot that tracks slashing events on the eth2 network. The bot also happens to be an homage to the legendary game and movie series Mortal Kombat. 

eth2REKT leverages the API endpoints provided by [beaconcha.in](https://beaconcha.in/api/v1/docs/index.html) to collect information on slashing events, and links the eth1 deposit addresses of the validator indices involved in each event to tags collected from [nansen.ai](www.nansen.ai) and [duneanalytics.com](duneanalytics.com). These tags might point to the `identity` and `activity type` of said address, and are maintained in a proprietary database that is updated periodically. 

The aim of this project is to help the community save time collating information around slashing events, in order to help propagate information that will ultimately make the network more resilient, and operators more accountable.

## How to read the tweets

eth2REKT’s tweets are drafted according to the following convention:
```
Validator [val_id] {id_tag | character | eth_wealth | abbr_depo_address} 
was slashed by 
validator [val_id] {id_tag | character | eth_wealth | abbr_depo_address | slasher_pedigree}

Condition: [condition]
Slot: [slot] 
Slash streak: [streak]

~ [MK_one_liner]
```
Below we explain what each of the variable fields represent: 

* `val_id`: the validator index of the slashed validator and the proposer/whistleblower that included the slashing proof equivalently
* `id_tag`: an approximation of the identity behind said validator index
* `character`: a heuristic on the type of activity this address has been involved in historically
* `eth_wealth`: a heuristic that points to the footprint of said address on the eth2 network (% ownerhsip). We provide with a table that explains the classification below
* `abbr_depo_address`: the abbreviated (5 first digits) deposit address associated with said validator index
* `slasher_pedigree`: a label that classifies the eth_address associated with said validator index, by the amount of slashes they have enforced over its active history of activity on eth2
* `condition`: qualifier of the condition that underlies each slashing event. “Double Prooposal” for proposer violations,  and “Double Vote” or “Surround Vote” for attestation related violations 
* `slot`: the slot that the slashes were included in
* `streak`: the number of consecutive slashes a specific eth1 deposit address has been subject to
* `MK_one_liner`: a series of Mortal Kombat one-liners taken directly from MK’s lore–because life is too short to take yourself too seriously. While these will be randomly generated for unrelated addresses being slashed, once the slash streak counter starts rising, they start following a different pattern to communicate the escalating situation. We outline the logic format below

On days when no slashings take place, the bot updates on how many days have gone by without a slashing event recorded on eth2. For example, for `n` days without a slashing event the bot will print:
```
n days, no slashing
```
## Eth wealth naming conventions

The taxonomy here is inspired by [glassnode.com's](https://insights.glassnode.com/bitcoin-supply-distribution/) work on BTC address taxonomy and is a work in progress. The following conventions apply on the respective tags:
|Tag        |eth_deposit_min   |eth_deposit_max   |
|:----------|:-----------------|:-----------------|
| leviathan | Top-10 depositor | Top-10 depositor |
| whale     | 20,000           | 999,999          |
| shark     | 4,000            | 19,999           |
| swordfish | 1,600            | 3,999            |
| octopus   | 320              | 1,599            |
| fish      | 64               | 319              |
| shrimp    | 32               | 32               |

## Slasher predigree naming conventions

Every time a validator slashes another, eth2REKT adds a `+1` on the lifetime count of slashes executed to the eth1 deposit address associated with said validtor. The following naming conventions apply to the different classes of lifetime slashes executed:
|Slashings |Tag          |
|:---------|:------------|
|1-5       |Noob Saibot  |
|6-10      |Reptile      |
|11-15     |Sub Zero     |
|15-20     |Scorpion     |
|20-30     |Prince Goro  |
|30-50     |Shang Tsung  |
|50+       |Shao Khan    |

## Slash streak naming conventions

When an operator (identified by their eth1 deposit addrress) gets slashed multiple times, the `slash_streak` counter rises. The following formatting conventions apply for a rising `slash_streak` count:
|Slash streak  |Tag                |Emojis                        |
|:-------------|:------------------|:-----------------------------|
| 1            | Random one-liner  | Random emoji                 |
| 2            | Toasty!           | 🔥🔥                          |
| 3            | Finish him!       | 🩸🩸🩸                   |
| 4            | Friendship        | 🌼🌱🎊🧸                  |
| 5            | Babality          | 👶🏻👶🏼👶🏽👶🏾👶🏿        |
| 6            | BRUTALITY!        | 👹👹👹👹👹👹              |
| 7            | FATALITY!         | ☠️☠️☠️☠️☠️☠️☠️ |
| 8            | STAGE FATALITY!   | 🩸🩸🩸🩸🩸🩸🩸🩸    |
| 9            | ANIMALITY!        | 🦙🐅🦑🐘🐍🐒🐁🐆                  |
| 10+          | Flawless victory! | 💯💯💯💯💯💯💯💯💯💯        |
