Monerotopia Notes

# Friday
- Opt-out talk by Derrick Broze
	- India's ADHAR system - actually Aadhaar - 12 digit personal ID 
	- There is almost always a tradeoff between privacy and convenience
	- Agenda 2030 was mentioned - think it's related to this: https://gravityofthings.com/what-is-the-great-reset-agenda-2030/
	- Freedomcells.org - peer-to-peer groups which self organize and govern
		- purpose to increase community
		- Seems like a half-baked "solution" to an unclearly defined problem. But sure, go connect with your community
	- cryptpad - claims to be e2e encrypted google docs
		- https://cryptpad.org/?trk=public_post_share-update_update-text
	- privacytools.io
	- https://theconsciousagora.com/
		- speaker's ecovillage project
	- "Agorism" is a flavor of anarchism - https://en.wikipedia.org/wiki/Agorism

- Global Opportunist's Handbook - talk from Juraj Bednar
	- General principle is to utilize "flag theory" taking advantage of various different jurisdictions of law for each need you have. For example, being employed in one country, recieving medical care in another, living in a third.
	- HCCP anarchist meetup...? Can't find info online
	- Paralelni polis
		- effectively a bitcoin-centric community in prague
		- https://www.youtube.com/channel/UCfHJ5Y3akQ7LA0PQmSYlYmQ
		- They host workshops, businesses, etc
	- You can see a recording of this talk where Juraj details which countries he uses and for what

- Bitcoin fog legal case
	- lawyers defending a presumably innocent dude who used bitcoin fog, from chainalysis which claims that this dude operated bitcoin fog
		- His name is Roman Sterlingov
	- Lawyers claim and explain how chainalysis is operating in league with US intelligence agencies
	- Exygent LLC was bought by chainalysis
	- Chainalysis has admitted that 90% of crypto mixer users were not engaged in criminal activity
	- A judge (who?) has declared that mixing crypto on its own is LEGAL
		- sets precendent that indicates this guy did nothing wrong
	- Chainalysis has refused to reveal information regarding supposedly traced transactions, claiming it is proprietary information
	- Chainalysis has relied on the accused taking guilty pleas, since typically fighting a legal case costs millions of dollars
		- this combined with not revealing how their blockchain software works, is how the chainalysis conviction machine functions
	- The CEO of kraken co-founded chainalysis
	- The legal firm giving this talk is taking on Roman's case without payment
	- Currenty attempting to obtain the actual evidence chainalysis claims to have

# Saturday
- View Balance keys
	- The idea is to see incoming and outgoing transactions for an account
	- This is interesting because currently there are only per-transaction (per TXO) view keys
	- View balance keys will be included in the Seraphis + Jamtis upgrade
	- Seraphis and Jamtis upgrade will increase the ring size from 16 TXOs to 128 TXOs
		- enhances privacy a LOT
		- currently it is somewhat possible to trace XMR transactions, and to be sure of your anonymity it is important to churn XMR TXOs a bit. This will make that churning requirement lower
			- Still, almost everyone is already safe enough with 16 ring size
	- View balane keys enables lighter wallets
		- wallets currently must scan the chain for viewable TXOs and Spent TXOs
	- The problem with current view keys is knowing whether those funds still exist at the recipient address or not
		- View balance keys will be able both incoming and outgoing, so they can effectively determine if funds were spent or not
	- important note - currently view keys (per transaction view keys) can also see a CHANGE output, which is an important and often overlooked privacy issue. 
	- Open question - should transactions/accounts with accessible view keys be marked and excluded from the possible ring set for future transactions? 
		- Problem here is that if a transaction is viewable, it cannot be a good decoy transaction within a ring later on. It lowers the anonymity set of the ring using it as a decoy
	- Open question - does doxxing spends reduce privacy for your recipient? How is this different from the current scenario of transaction view keys
	- There's a little known tool to prevent spends of certain outputs called "blackball"
		- you can basically burn your funds and "blackball" them...?

- GrapheneOS
	- only for google pixel
	- sandbox mode prevents apps from doing data collection on your device
		- can turn off sensors or feed those apps garbage data
		- Sandbox mode is basically a wrapper for any app available on the play store - it runs in the "sandbox" which, to google, looks just like a regular phone environment
	- Suggestion from group to go for a google pixel 6 or above, since security updates will get pushed for longer and since Graphene can leverage those
	- once setup with GrapheneOS, one should "lock the bootloader"
		- apparently if plugged into a malicious device, they may be able to utilize the bootloader to access boot or root
	- grapheneos.org
	- multiple profiles can exist on phone - like users on a PC
		- notifications can be passed across profiles - so you can get notifications from one profile while logged into another
	- apps can be installed cross profile - referencing the same app binaries but with data localized to each profile
	- sensor toggles - turn off camera on firmware level, as well as mic, accelerometer, GPS etc. Virtual switch which disconnects sensor from CPU
	- deadman switch reboot or auto-reboot - tell the phone to reboot or revert to factory if you don't log in after X time

- Seraphis Dev Talk
	- Add an "unspent proof" to the protocol. So far the protocol pretty much just has spent proofs
	- there's a seraphis paper by github user UKoeHB (Koe)

- Chainalysis Panel
	- Chainalysis wasn't there, it's just the lawyers and other monero folks
	- Chainalysis develops "risk scores" but they are IGNORANT (allegedly)
		- methodologies for those risk scores are hidden 
	- Breadcrumbs.io is another blockchain tracing organization
	- Different firms have wild ranges for the percentage of BTC transactions that are "illicit"
		- between 0.4% and 12% depending on who's talking
	- Some insider allegedly has stated that chainalysis's entire business is a fraud, they simply are in good with US lawmakers 
	- Historically, new forensic methods tend to have lots of false positives while they are new. For example, DNA evidence.
		- Why should chain analysis be different?

- Side conversations
	- someone recommended NJAL.LA for anonymous hosting
	- privacytools.io is a favorite round here

- Haveno talk
	- "Monero Native Bisq"
	- Currently struggling a bit with pricing for XMR, its difficult to reach decentralized consensus on the XMR price
	
- ETH<>XMR atomic swaps
	- Live now!
	- On mainnet
	- Beta
	- Swaps take about 20 mins
	- ERC20 support (is planned? Is already implemented? It definitely WILL exist, may already exist)
	- uses basic key combination math for XMR and ETH 
		- simple multiplication and addition of keys to do crypto magic
	- uses libp2p library for nodes to connect with others
	- one early iteration was not frontrunning protected
		- curious to see how frontrunning posed a problem here
	- They mentioned they have a matrix chat - this was also somewhat popular at monerotopia. 
		- I should go check out matrix
	- github: AthnorLabs/atomic-swap

- Cypherpunk talk
	- different strategies are often posed to fight hierarchies which is what we typically exist in
		- submission, dominance and reorganization strategies are often posed, but don't work well to fight hierarchies
		- instead, just leave the game. Don't try to change it
	- Dropping off the radar is best from a personal point of view
		- Opting out results in no feedback - it will be unclear if you are "winning" or "losing" the game
			- but that's not the goal anyway (see "leave the game")
	- Opting out allows for self discovery. What are YOUR goals rather than the goals of the game?
	- Opting out draws less attention which may be negative
	- OODA loop: observe, orient, decide, act
	- "Cryptoanarchy" prevents conflict via technology
		- it breaks the link between actions and a physical body
			- physical body is often what is punished or the object of some conflict 
		- anonymity, encryption are tools or cryptoanarchy
	- "Seeing like a state" book
	- "against the grain" book
	- To the "fiat world" you should appear like a backpacker having the time of their life, maxing out daddy's credit card
		- have no income or property (seizable or threatenable)
		- no tax revenue (no profit incentive for a government)
	- Be aware that the state will see with great detail all border crossings, all license plate scans, all transactions which hit bank accounts
	- keep your communications private
		- communications include transactions which hit your bank account
	- be "too small to fail" - don't rely on any institutions for anything you cannot lose overnight
	- money acts as a "thank you note" for the good deeds of society
	- register yourself as a business to save money
		- the speaker disagrees because you're still using dirty fiat
	- don't threaten "the game" - it makes you a target for those who are still playing
	- "searching for gamma" blog post
	- "cryptocurrencies: hack your way to a better life" book
		- I bought a copy
		- details, among many things, how to account for a business or personal budget with crypto
		- utilize futures in a fancy way to spend crypto when its at high prices, allowing yourself to achieve a small discount on stuff paid in fiat

- Side convos
	- Monero CCS is where devs get funding
	- "Magic" organizes monero dev funding

# Sunday

- Talk about privacy efforts on bitcoin
	- Go check out "breaking monero" on youtube
		- dissects the limits of the privacy properties and the technical design of monero
	- Go see how bad BIP47 is
	- Samurai wallet hosts a centralized server which matches human readable addresses with bitcoin addresses (privacy issue)
	- BIP47 (private sends of some flavor) requires a notification transaction prior to private sends. Reveals some info and is bad UX
		- "silent payments" do not require this
	- Lightning can offer good privacy or poor privacy dependent on lots of things including other actors on the network you may have no control over
		- additionally an on-chain tx is necessary to open a lightning channel
		- large lightning nodes are often centralized entities
	- RingCT (monero uses this) is less powerful against targeted surveillance
		- it's relatively easier to trace one specific payment/actor through ringCT than it is to trace EVERY payment through ringCT
		- check out breaking monero for info
		- this is why monero requires churns if you want to ensure privacy for yourself
		- ringsize increase helps
	- For recieving bitcoin, most private method is still manual address sharing over secure channels
		- if you are super savvy and have very good coin hygiene, you can use "payjoin" (not coinjoin)
	- Privacy on bitcoin has fungibility problems - there are signs that a TX utilized a privacy enhancing technology, and that reduces your anonymity set and makes your tx easier to single out
	
- Talk from Firo
	- Firo is a rebrand of ZCoin
	- not zerocash, zeroCOIN (zerocash is apparently different)
	- privacy works by burning coins, then re-minting them later in the future via a ZK Proof
	- There were issues with zerocoin in the past with a cryptographic flaw not caught by peer review (we're cypherpunks, remember? There were like 5 people who understood the math at all). This affected many different forks and eventually resulted in tarnished image -> rebrand
	- Lelantus V2 brings back the burn->redeem mechanic
	- there are no fixed denominations like with tornado cash for example
	- the anonymity set is limited to ~65k transactions
		- should be enough
	- "no recipient privacy" - dunno what this means
	- no multisigs
	- Typtich separates value & membership commitment (sorry i forgot what that means)
	- Spark expands the technology to work with assets AKA tokens
		- additional assets adds to the anonymity set
		- so basically Firo supports private tokens in addition to its native asset
	- outside assets are bridgeable into the protocol
	- "aura" is a privacy-preserving voting protocol
		- The Deomocrat Party Election of Thailand used aura
	- Firo.org
		- goal is a general purpose privacy-focused infrastructure for crypto

- Talk from Oxen
	- Session - getsession.org
		- signal competitor
		- uses private/public keypair for identifier rather than phone number
	- Lokinet - handles complex and high bandwidth applications privately
	- current problem is app monetization - apps are free to use (Oxen has stated support for this) but of course, compute resources aren't free
		- Oxen has stated a goal to never rollback the abilities of "free tiers" of software
	- `alexlinton` on session or `alexblinton` on twitter

- Monero's Ethos
	- Create the best digital CASH
		1. privacy
		2. decentralization
		3. low barier to entry - CPU mineability
		4. Proof of work to prevent special status of different nodes (higher voting weight due to ownership)
	- No cap on supply is by design, not sure why

- "Spats"
	- private design for multi-assets
	- single asset means fungibility and a single total supply
	- multi-assets mean there are separate total supplies within the same system
	- BCA = Bitcoin Confidential Assets
		- coins are represented as masked commitments with a "value" and a "secret mask"
		- each commitment takes up a slot, meaning you can reveal only one asset even if multiple assets are involved in a transaction
		- "asset surjection proof" - proves asset type is allowed
			- this is very bulky/slow though
		- Every asset needs its own range proof
		- this encountered problems with NFTs - you could only prove ownership at some point, but not now (revealing recieving of NFT, but unless able to reveal all other transactions you can't prove you own it NOW)
	- spats allows for ownership proofs which are accurate for a given time
	- Was designed to work with Spark (Firo i think...?) but may also work with Serpahis (Monero upgrade)
	- spats adds two slots to a transaction:
		- for XMR we have "value" and "mask"
		- for spats we have "value", "asset", "id", and "mask"
	- Spats only requires one range proof
	- NFTs and FTs are treated similarly, NFTs just have a total supply of 1
	- the number of different assets within a transaction is exposed with spats
	- Pain point is the fee in a single denomination
		- this is TBD whether it should be possible to pay fees in mulitple currencies
	- Seraphis (monero) and Spark both add "linking tags" to each coin
		- this tag simply flags the first spend, to avoid double spends
		- "linking tag" = "key image" in XMR
		- searching for a tag allows someone to determine if a coin has been transferred
			- in XMR this tag must be revealed before you know it (so you can selectively reveal current ownership)
	- Fee side and asset side are not linked so that revealing one doesn't impact the other

Particl 
	- Adaptor Signature Swaps 
		- Untraceable
		- requires at least one coin to have segwit enabled
	- SMSG message protocol - each message is stored on every node, but it's encrypted
		- this powers orders on basicswap
		- orders can be encrypted such that they are only readable by selected parties
		- the order maker must have an SMSG node that stays online for the entire swap
			- seems bad IMO
	- Particl marketplace is basically eBay but with XMR
		- requires the Particl stack to be running in the background
		
# Recordings:

- Friday, May 5th:
	- LIVE STAGE: https://streamyard.com/2qpg5487w6vc

- Saturday, May 6th:
	- LIVE STAGE (PART 1): https://streamyard.com/282bigedd4t8
	- LIVE STAGE (PART 2) https://streamyard.com/6nhxyc8fr7hn
	- REMOTE STAGE: https://streamyard.com/kkub3bff57rz

- Sunday, May 7th:
	- LIVE STAGE: https://streamyard.com/zyshhd3mu5aw
	- REMOTE STAGE: https://streamyard.com/3ee7eiqa3rhb


