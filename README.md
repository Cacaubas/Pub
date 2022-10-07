Forum publico for sharing a cookbook

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
Para este exercicio um Forum publico foi criado usando comandos freechains.


1. starts the local peer to serve requests 

$freechains-host start /tmp/freechains
   
2. Create an identity

(Switch to another terminal) foi realizado em dez terminais

$freechains keys (pubpvt) <passphrase>

3. Prepares host to serve a chain

$freechains keys (pubpvt) <passphrase>

4. Post some contents

$freechains chain '#receitas' post inline "Receitas faceis"
1_DE2EF0...

At this point the Forum is created.
#
From then, start others freechains hosts. (were created ten hosts)

$freechains-host --port=833(1/2/3/4..10.) start /tmp/othost_(1/2/3/4...)

1. Create an identity: 

$freechains keys pubpvt <passphrase>

2. Join the public forum using the private keys

$freechains chains join #receitas <private key>

3. Synchronize with the first host 

$freechains peer <host:port> (send | recv) '#receitas'

Iterate over posts in a chain:

Shows the consensus order of posts in the chain.
Reads the posts payloads.

$ freechains --host=localhost:8331 chain '#receitas' consensus

0_C40DBB... 1_DE2EF0... 2_317441...

#
Reads the posts payloads

$ freechains --host=localhost:8331 chain '#receitas' get payload 1_DE2EF0...

Brigadeiro

$ freechains --host=localhost:8331 chain '#receitas' get payload 2_317441...

Bolo rapido

#
Gets the reputation of block (public key), more reputations means that the block has been tested and approved.

$freechains chain '#receitas reps  <hash of block>

#
Using  Likes block in the chain.
   
$ freechains chain '#receitas' like '3_51C7BD...' --sign='<my-pvtkey>' --why='A receita bem facil'

Using to simulate the passage of time of nodes.

$freechains-host now <timestamp>
   
188516584433068609
   


