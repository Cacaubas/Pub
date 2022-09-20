Public Forum created for content disseminated using Freechains

Freechains is a permissionless peer-to-peer publish-subscribe content
dissemination protocol.

- A user posts a message to a chain (a topic) and all other users subscribed to
the same chain eventually receive the message.
- Users spend their reputation to post new messages and gain reputation from
consolidated posts.
- Users can like and dislike messages from other users, which transfer reputation
between them.
- The resource timestamp indicate the age of the peer in the chain. 
#
For this simulation a public forum was created using freechains commands.

1. starts the local peer to serve requests 

$freechains-host start /tmp/freechains
   
2. Create an identity

(Switch to another terminal)

$freechains keys (pubpvt) <passphrase>

3. Prepares host to serve a chain

$freechains chains join '#pub' '<private key>'

4. Post some contents

$freechains chain '#pub' post inline "my contents line 1"
1_DE2EF0...

At this point the Forum is created.
#
From then, start others freechains hosts. (were created four hosts)

$freechains-host --port=833(1/2/3/4...) start /tmp/othost_(1/2/3/4...)

1. Create an identity: 

$freechains keys pubpvt <passphrase>

2. Join the public forum using the private keys

$freechains chains join #pub <private key>

3. Synchronize with the first host 

$freechains peer <host:port> (send | recv) '#pub'

#
Iterate over posts in a chain:

Shows the consensus order of posts in the chain.
Reads the posts payloads.

$ freechains --host=localhost:8331 chain '#pub' consensus

0_C40DBB... 1_DE2EF0... 2_317441...

#
Reads the posts payloads

$ freechains --host=localhost:8331 chain '#pub' get payload 1_DE2EF0...

my contents line 1

$ freechains --host=localhost:8331 chain '#pub' get payload 2_317441...

my contents line 2

#
Gets the reputation of author (public key)

$freechains chain '#pub reps <public key>

In first day, as only the Forum's creator had reps, only his blocks has been appeared in consensus questions 
#
Doubts:

In 24h, the reps of Autor was increased, but only one other user had his reps incresed. 

Other situation that i didn't be able to explain was the fact that the blocks in this chain hadn't their reps increased.
