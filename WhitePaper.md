# PDU - A decentralized identity-based social network

This copy is translated by [Google Translate](https://translate.google.com/) [中文白皮书](https://github.com/pdupub/Documentation/blob/master/zh-CN/WhitePaper.md)

* email: hello@pdu.pub
* wechat: pengpengt00
* twitter: [@PDUPUB](https://twitter.com/pdupub)

[![License](https://img.shields.io/badge/license-GPL%20v3-blue.svg)](LICENSE)
[![Chat](https://img.shields.io/badge/gitter-Docs%20chat-4AB495.svg)](https://gitter.im/pdupub/Welcome)

**Abstract:** Social network services (SNS), such as Facebook, twitter, and WeChat etc, which users can create identities on the platform, maintain connections and exchange information with each other. However, those SNS rely on a centralized network service provided by the company or organization, which makes it easy to be controlled or blocked. The BitTorrent protocol can implement P2P information exchange, but its original purpose is to improve the transmission efficiency of known data, and its weakened account system design is not suitable for uncertain information exchange. For a decentralized system, even if a digital signature can prove the source of each information, due to the lack of third-party verification (such as mobile phone number registration) to give account creation costs, the useless information will flood the entire network easily, the information source cannot be punished.

We propose a way to make sure account creation costs in a pure P2P environment, and based on this account system, build a complete P2P social network. First, we construct an order by reference to prove that a particular behavior occurs after a certain behavior, that is time proof. Then, the time interval between the creation of a new account must be jointly confirmed by multiple existing legal accounts and such confirmation of the same account must be met. Users (including non-users) of each account system can maintain the relationship topology between some or all of the accounts of the DAG structure. new accounts can be verified at any time based on the information they have learned. Evil acts punish certain accounts and related accounts. Users do not need to agree on all behaviors, nor do they need to maintain consistent information.

<!-- MarkdownTOC depth=4 autolink=true bracket=round list_bullets="-*+" -->
- [Introduction](#introduction)
  * [Background](#background)
  * [PDU](#pdu)
- [Message](#message)
  * [Message Credit](#message-credit)
  * [Message Sequence](#message-sequence)
  * [Time Proof](#time-proof)
  * [Spacetime](#spacetime)
- [Account Topology](#account-topology)
  * [Family relationship](#family-relationship)
  * [Life Cycle](#life-cycle)
  * [Natural Law](#natural-law)
  * [Account Creation](#account-creation)
-[Currency system](#currency-system)
  * [Scope](#Scope)
  * [Equity Attribution](#equity-attribution)
  * [Anonymous Transaction](#anonymous-transaction)
  * [Evolution of DPOS](#evolution-of-DPOS)
  * [POW compatible](#POW-compatible)
-[Network](#network)
  * [Network Model](#network-model)
    + [Account Location](#account-location)
    + [Message Space-time Distance](#message-space-time-distance)
  * [Message Propagation](#message-propagation)
  * [Function Node](#function-node)
    + [Time Proof Node](#time-proof-node)
    + [Account Information Node](#account-information-node)
    + [Account Status Node](#account-status-node)
    + [Message Distribution Node](#message-distribution-node)
-[World Creation Process](#world-creation-process)
-[Conclusion](#Conclusion)
<!-- /MarkdownTOC -->


## Introduction

### Background

Most information dissemination and interaction on the Internet today rely on a powerful and trusted third-party centralized service, such as social networking services such as Facebook, Twitter, WeChat, and Weibo. Its existence has undoubtedly brought great convenience to users, but with its gradual development, the problem of centralized social services has gradually emerged.

1. Whether intentionally or unintentionally, there is a possibility that third-party services may use user information or cause leakage of user data. (FB)
2. For commercial considerations, centralized service providers will use their strong user base to suppress competing products, such as restricting the spread of information about their products on their own platforms to maintain their monopoly position. (Wechat)
3. Centralized services are subject to government supervision and blockades. (GFW)

But even so, due to the reliance on three-party centralized services, many users still have to choose to continue to use the service that has the problem instead of migrating their own data. Because for most users, although leaving a certain platform will not lose their own data and information, they will lose the long-term user relationship accumulated on this platform and their own credit value on this platform.

In essence, the root of this problem is that the user group itself cannot form a network that is separated from a third party, so the user's relationship information belongs to the platform rather than itself.

### PDU

We propose a new type of social network (PDU) based on a decentralized account system, which also excludes third-party centralized services. Instead, we hope that through the implementation of the decentralized account system (DID), the user identity can be The confirmation and relationship topology is separated from a specific platform to eliminate the user's dependence on a specific third-party centralized service, so that the user's identity and social relationships truly belong to the user.

Just as **double spend** can be considered as the fundamental problem to be solved in a decentralized currency system, the fundamental problem to be solved in a decentralized account system is how to give the necessary **costs** to account creation, so that Its controllable.

We modeled nature and society, first introduced the concept of time proof, and based on this we formulated the laws of nature. New accounts created in accordance with the laws of nature may be accepted by other users (some users) in the system. Each user can use the structure of a directed acyclic graph (DAG) to maintain all the users he **recognizes** and the parent-source topological relationship they constitute. Any message that violates the laws of nature will be transmitted as evidence in the network, allowing the message receiver to punish the malicious user according to the local source-source topology. The depth and breadth of the source of the punishment account shall be determined by the recipient.

Different from the traditional centralized service account system, the natural law of PDU also defines the life cycle of the account based on time proof, so that unused accounts can be naturally eliminated, and the total number of accounts increases linearly. ), And the number of users in the current life cycle will be approximately constant.

Proof of time is the basis of cost control for all actions of users in the PDU, but because there is no mandatory consensus in the PDU, it is the user's own choice, so it is entirely possible that there are multiple different time proofs. PDU accepts the existence of this situation, just like multiple space-times that usually exist, and even each space-time can set a different time flow rate to affect the behavioral cost of this space-time. At the same time, any user can exist in multiple time and space of his choice.

## Message

Message specifically refers to the information with digital signature in the PDU. This simple structure is the basis for constructing a P2P network structure.

Accounts (and their users) can and can only implement all network behaviors in the sole form of sending messages. If this network is viewed purely from the perspective of information dissemination, the real-time value of an account can be measured by the reach (how many accounts are accepted) of each message it produces.

Whether each message can be accepted by an account (different from the information received, acceptance means that the received information is verified and considered legal) is entirely up to the recipient. Therefore, each account constructs the entire PDU network from its perspective through the selection of the received information. In other words, the range of information accepted by the account itself determines the time and space of the account.

The content of a message can contain one or more other messages, or even multiple levels of nesting, which we call **references** .

### Message Credit

Since the information produced by each account is received, or the degree of its spread is completely determined by the recipient, there is no specific centralized three-party platform to ensure the spread of the message, and there is no consensus mechanism to ensure the entire P2P network Both agree to accept or reject a message. The basis for judging whether or not to receive a new message comes from the subjective determination of the creditworthiness of the source account and the credibility and real-time nature of the message itself. The producers of information will naturally try their best to comply with the rules of the PDU system (pleasing the audience) in order to increase the spread of the produced information to improve the credibility of the message.

Due to the existence of digital signature technology, even in a P2P network environment, the source of information can still be easily confirmed between accounts, but how to determine other attributes of the information? We find that in the real world, our judgment of information often has a subconscious discrimination condition, which is time. When an individual produces two conflicting agreements with two individuals, we will take the agreement that occurred first and determine that the individual that caused the conflict is not credible. When we receive multiple information about an event, we update what we think is the current state of the event based on the latest information. We are used to making such judgments because time is unidirectional, which gives information an orderly nature, and our judgments are essentially based on this.

### Message Sequence

First of all, not all messages in the PDU must be ordered, and not every account needs to construct the messages it produces into an ordered form. But as a whole PDU, because the content of the message itself can refer to other messages, when the above situation occurs, it will naturally give order to the message. We can think that the quoted message must occur before the message that references it. .

When each new message of an account in the PDU refers to the previous message of the account, it will naturally constitute a message queue of the account. We call such a message sequence self-certified and orderly. However, the problem that arises is that the new message will contain all the content of the previous one, resulting in an increasing content of the message. In practical applications, we can use the hash value of the message content instead of the message content for reference.

In the real world, if we want to prove that something happened after a certain time, the easiest way is to find a newspaper of the day and take a picture together. Publishing this picture is obviously more persuasive to the public than publishing your diary. Therefore, in the PDU, any message can also refer to messages from other accounts (more trusted) to prove the orderliness of the messages issued by itself. We can call this method the order of evidence.

Because each message can refer to multiple messages, in order to improve its orderly credibility, a message can contain self-certified and orderly references and multiple other orderly references.

### Time Proof

Strictly speaking, any message published by any account can be cited by itself or other accounts as proof of time. However, the following problems will occur in actual use:
1. If a message is published infrequently, it will affect the accuracy of the time it is used to testify.
2. If it is too frequent, it will reduce the cost of account creation that relies on this time proof.
3. If the message can be fully grasped by the publisher, it will affect its scope of use.

For the situation described in point 1, the account owner can easily control the frequency of his own news release. If he wants to become a more widely accepted time proof account, he will provide stable services and publish messages at a fixed periodic frequency. . (Conducive to make this account more widely accepted and improve the news to a wide range)

The impact described in point 2 will be described in the next chapter.

Regarding point 3, the account owner should propose a certain message designation mechanism to make other accounts believe that the messages they publish are more random. For example, by providing an external interface, any user can submit data through it, and the account owner puts all the information received in the time from N to N + 1 into the content of the message released at the time of N + 1.

### Timespace

Different time proofs will be used to construct different spacetimes, so even if multiple references to time proofs are included in the same message, the purpose is only to make this message legal in multiple time and space, and does not mean more What is the relationship between this time proof. At the same time, the time proof does not specify the true time interval between two adjacent blocks.

The right to choose time proofs is in each user. Users can choose one, multiple, or no time proofs at all, or they can choose different time proofs in their multiple messages. However, it is recommended that users try to choose a time credible with high credibility to set up a time credential for their actions, in order to prevent the credibility of the time credential they use due to the instability of the account that issued the time credential or malicious behavior.

For publishers of time proof:
1. Whether messages posted by this account exist as proof of time by other users is up to the adopter, not the publisher.
2. The time proof belongs to the message, and it is only visible to other accounts in the time and space to which the account belongs.

## Account topology

The account system is the basis for all user behavior in social networks. Based on the account, social relationships can be established, authentication actions can take place, and users can receive rewards and punishments for their own actions. When the account system is maintained by a centralized platform, the account creation process and use process are based on this platform, so it is easy to control and effectively limit some malicious behaviors. For example, the behavior of creating a large number of accounts for a single user, the platform can increase the cost of creating an account by binding real-world information, such as mobile phone number verification. In order to cope with identity fraud and theft, the platform will force users to use more complex passwords during the registration process, shorten the expiration time of login, and strengthen the security level of their platform. In order to deal with the malicious behavior of users, the platform will specify some rules and regulations. When the user violates certain rules, the platform will punish the user. These punishments are not necessarily known to the user, such as only reducing the probability of revealing their information. , Or delete all its information completely. It can be seen that the control right of the account system lies entirely in the platform on which it depends. When this platform is fully trusted, this is a good solution, but if there is a fully trusted centralized platform, the answer is obviously negative of.

Due to the existence of digital signatures, even in a completely P2P network environment, there is no problem with information authentication and confidentiality. The user's identity is based on an asymmetric key pair, the information producer uses the private key to sign the information, and the information recipient uses the producer's public key to verify the authenticity of the information source. For encrypted content, the producer can encrypt the recipient's public key, and then use the producer's own private key to sign. The information receiver receives the information, first uses the counterpart's public key to verify, and then uses its own private key to encrypt the content. Decrypt.

However, due to the easy creation of asymmetric key pairs as the basis of identity, a single user can also create a large number of key pairs in a short time. In the P2P network environment, in order to control the number of legal accounts based on key pairs and increase the cost of account creation, we first proposed two concepts of parent-source relationship and life cycle based on time proof, and defined multiple Laws of nature. Each user in the P2P network can determine whether to accept the existence of the other party according to his judgment of other users.

### Family relationship

The parent-child relationship refers to the relationship between two accounts. In the PDU, all legal accounts of **single space-time** recognized by each node have direct or indirect parent-child relationships. With the exception of the two genesis accounts, all accounts have and only two parent accounts with different attributes. The relationship topology formed by the entire account system is a directed acyclic graph (DAG) initiated by two genesis endpoints

### Life cycle

Each account has its own life cycle based on time proof. The life cycle of this account starts when two different attribute nodes complete the signature and broadcast the time proof of this event. Only messages produced by an account during its lifetime can be considered legitimate. (* Because the node receiving the information will be more inclined to keep up-to-date and highly credible news, after the end of the life cycle, it is not significant to falsify historical messages for broadcasting.

The length of the life cycle is related to the parent account, but it is not lower than a certain value, which is the minimum life cycle.


### The Law of Nature

1. Each account has a binary attribute. The attribute value is determined by the end parity of its public key. The two accounts of creation must be different attribute accounts.
(*This provision means that users can choose this binary attribute by repeating the process of generating asymmetric key pairs. The secondary binary attribute of this account system will not approach uniformity, because when one party becomes rare At this time, due to the signature rules of the parent address, more rare addresses will be selected to increase their account value.*)
2. Each newly created asymmetric key needs to undergo a signing process, be signed by two legally different attribute account lines, and then broadcast to the entire P2P network before it can be recognized by other accounts.
3. The parent address of the signature execution must have experienced at least 1/4 of the minimum lifetime before the timestamp contained in the signature.
4. The parent address of the signature execution must have at least 1/4 of the **minimum life cycle** before the time stamp included in the signature, and no other new account signatures have been created.
5. The two signature accounts with different attributes are signed before and after, and the content of the second signature must include the first signature.
(*The order of signatures of two different attribute parent addresses is not enforced for the time being, but it may be expanded in the definition of natural law in the future to further increase the cost of creating an account*)
6. The length of the life cycle is related to the parent account, which can be defined as 1/2 of the account with a longer life cycle in the parent account, but not less than the minimum life cycle.
(*The setting of the life cycle is conducive to the expansion of the system account through the control of the time-proven flow rate at the beginning of the entire system. At the same time, when the system account reaches a certain number, the number of all currently active accounts is controlled.*)
7. The life cycle of a child account is calculated from the completion of the signature on the second parent account that executes the signature, the proof of time contained in the account.
8. Two parent addresses performing signatures cannot be direct or indirect parent-child relationship accounts.
(*Introduced this algorithm into the calculation of the account's public address, but it can also be understood as, in the process of creating a new account, we must introduce new genes.*)

The behavior generated by the signature also belongs to the general message (Message), and its form, transmission method and trustworthiness are the same as the message.

Legend to be added ...

### Account Creation

In the process of creating an account, the process of generating basic account information for a new account is usually not structured such that the message is transmitted in the PDU, because the account to be established at this time is not legal, and other accounts will not accept such messages. The two accounts required by the cosign process have a sequence. The system only requires the parent address of the post-signature to construct the account information to be built and the content superimposed twice into a message, which is broadcast on the network. The first The signed address does not have to broadcast the signed message. However, since the two signatures must be accompanied by time certification, even if an account is the first signed account in the process of creating an account and has not sent a message, if it is found that the signature time of the two account creations is less than 1/4 This minimum life cycle will still be broadcast and punished as an Evidence Message.

The account creation process is as follows:
1. The new account A creates a key pair and provides A's public key to the first account B that meets the signing conditions for signing. This process usually does not pass through the message system of the secondary PDU network, because the new account A is not yet legal for other accounts at this time.
2. After account B signs A's public key, the signed message can be provided to another signed account C in any way. C and B must be accounts with different attributes.
3. Account C signs the message signed by B and broadcasts the message.
4. The node receiving the broadcast will verify whether the cosigns of B and C are legal. If it is legal, add A to the account relationship topology map maintained by itself. (Similarly, if illegal, collect evidence of evil and broadcast it.)

Regarding the case where the same public key is separately signed by multiple private keys, it is also allowed in the system, which is equivalent to creating multiple accounts with the same password.

## Currency system

For a network system abstracted from the natural society, the currency system is obviously a very important and necessary subsystem. But a social network based on a decentralized account system obviously cannot rely on some kind of centralized currency. When it comes to a decentralized currency system, the first thing that comes to mind is necessarily built by the blockchain represented by Bitcoin. Point-to-point electronic money. This section mainly discusses the similarities and differences between the currency system constructed in the PDU and a completely independent currency system, and the way in which the currency system is constructed in the PDU.

### Scope

Currency in reality has a scope, usually a country or region will issue and circulate a certain currency. For example, you can use the US dollar in the United States, the euro in most parts of Europe, and the renminbi in China. Although major currencies such as the US dollar are recognized in many countries, they often need to be converted into local currencies during use. In addition to the scope of the region, the scope of time is usually ignored by us. Money hundreds of years ago is basically not recognized now, even if it may have higher value as a cultural relic.

Before building a currency system in PDU, we need to make clear the following points:
1. All information is based on messages, and messages are only valid in the time and space to which the message publisher belongs.
2. For a blockchain-based currency system, the news of building its system is the release of each block.
3. We consider a block valid only if all blocks can be continuously verified.

It is easy to deduce from the above three points: **A currency system composed of a blockchain has the scope of the space-time where all block producers are located and the space-time divided by it.**

### Equity vesting

One public key can generate multiple account addresses in the same space-time, and the messages of multiple account addresses are controlled by the same private key. The equity in the monetary system also belongs to the private key owner, which is equivalent to the equity belonging to all accounts controlled by this private key within the effective time and space. If the source of the message received by the miner is not considered, it can be considered in a broader sense that as long as the corresponding private key is possessed, the currency control right corresponding to the private key is possessed.

### Anonymous transactions

The account address corresponding to the currency system constructed in the PDU can also be different from the account address of the PDU, and only corresponds to a private key in a specific format, and the encryption method can be determined by the currency type. In this case, we treat the address as part of the message, not the PDU address. Signed transaction information can be published by any three parties. The specific steps are as follows:
1. The charging party encrypts the address and information with the paying party's public key and sends it to the other party.
2. The payer assembles the transaction as required and adds a signature.
3. The payer sends the signed transaction to any third party for broadcast.
4. The transaction is accepted, but other than the charging party and the paying party, other users can only understand the existence of the transaction through the information, but it is not clear which account the charging address (non-PDU address) belongs to.

### Evolution of DPOS

DPOS is a consensus mechanism adopted by blockchain projects such as EOS. Its essence is closer to the way in which transactions are handled in real society. Interested groups regularly elect representatives in a certain way, and these representatives handle the affairs in a relatively centralized manner. Stakeholder groups can monitor and regularly change their choices. In order to avoid being too centralized, the number of delegates and the operation mode are also specified in DPOS. Compared with the consensus mechanism of POW, its efficiency is higher.

However, in a completely independent blockchain system, because there is no cost to create an account, in the election process, the measure of the number of votes is the amount of currency held (which can be weighted according to the holding time). However, the problem with this method of operation is that only the current holder of the currency can determine the generation of the representative, and the currency's liquidity and the stability of the representative will become contradictory. Potential users who hope to have a stable currency system cannot express their suggestions, and Short-term currency holders may not care about the long-term stability of the currency system.

In the PDU, due to the introduction of account creation costs, the DPOS consensus can improve the fundamental issue of elections. The meaning is not to completely abandon the number of votes calculated by currency ownership. The process can arbitrarily select the optimal matching ratio on the straight line from one person, one vote to one yuan, one vote, and find a moderate equilibrium point. Or set up multiple different currency systems in the same time and space for users to choose.

### POW compatible

POW's block producers do not require identity verification, so any account can post the content of a block as a message. So whether it is to build a new POW consensus blockchain in a space-time or to introduce existing bitcoins (specifically the current bitcoin main chain, the longest chain), it only needs to satisfy all the regions on a chain Block messages that can be found (or considered to be found) in this space-time can be considered as valid for this chain.


## Network

### Network Model

In the PDU system, all user actions are realized through messages, and the network (Network) is the path selection for message propagation.

Before going any further, we need to be clear about the impact of time and space on accounts and news. When an account a is created, its parents reference several time proofs during the cosign process and are verified to be legal. The new account exists and only exists in these space-times. We temporarily call this space-time set A. Each message published by this account a can refer to all or part of the time certificate in the set of time and space A as a reference, and it can also exist in the message sent by account b in one or more of the time and space set A. As proof of time. a can even refer to the message published by account c that has no intersection with the space-time set A in its own message (* but this is meaningless because a does not exist in the space-time of c * ). It can be seen that any account or message may exist in multiple time and space at the same time, and the cases that belong to multiple time and space can be regarded as the superposition of multiple single time and space and processed one by one.

#### Account Location

After the account is created successfully, a hash value (sha3-512) can be calculated based on the creation message, which is used as the account address. And this account will share this address in all of its legal existence time and space. This address will also be used as the basis for calculating Account Location to affect the dissemination of information.

In a P2P environment, each account is completely equal, and there is no essential difference. Therefore, the position of the account in the network needs to be calculated based on the account address to meet the following conditions:
1. The positions of accounts in the entire network are evenly distributed.
2. There is no center or boundary in the distribution.
3. Account position is in a limited range.

The simplest way to achieve the above characteristics is to map a low-dimensional space to a sphere in a high-dimensional space, and the dimensions and scales can be selected by each account. In the process of network propagation, if the account has a constant dimension and chooses a continuously changing scale, you will see a high-dimensional space that gradually expands or contracts, and the nearby account will move with the change of space. . If the account selection dimension changes or the discontinuous scale changes, the account in the nearby location will have a jump-like change.

For example: Suppose that the address of an account is only a decimal number 2418. To calculate his position, we choose 2 dimensions. First, it can be projected onto a two-dimensional plane with x-axis coordinates of 24 and y-axis coordinates of 18. Next select the size of the sphere. Assuming a sphere with a maximum perimeter of 7, you can think that the address of this account is mapped to the position on the sphere (3, 4). We can calculate the positions of all known account addresses according to the same dimensions and scales, and then use the coordinate distance between us as less than 1 as the neighboring address to achieve the propagation of the message.

The above example is a two-dimensional example, but in real applications, we can choose a higher dimension for position calculation.


#### Message space-time distance

The message distance (Message Distance) is usually used by the receiver of the message to determine whether it will be forwarded according to the nearby account. (It has nothing to do with the user seeing a message, and therefore interested in it.)

Distance of message ^ 2 = sum (distance in a certain dimension ^ 2)-(vt) ^ 2

Where v can be set according to the account's sensitivity to the real-time nature of the message.

### Message Propagation

The complete message propagation process has the following steps:
1. Produce **message content** and quote one or more other **messages**. (Using messages from this account can achieve ordering of its own messages, and messages from external accounts can be regarded as proof of time)
2. Send a message to the established **adjacent account**, or send this message to the account address of the specified target.
3. An account address verifies the message signature after receiving the message. If the signed account is not in the local DAG relationship topology, the current account can choose to request information from other account addresses to improve its relationship topology before processing the message, or it can be abandoned This message. (* When forwarding messages from other accounts, this account is usually maintained in its own parent-source relationship topology, and can respond to other accounts' requests for related parent-source information. *)
4. Process the message content.
5. Optionally forward the message to **Near Account** .

If in step 4 you find evidence of a message that violates the laws of nature, punish the relevant malicious account, such as refusing to accept subsequent messages from this account, and broadcast the evidence of evil. You can also punish other related accounts according to the relationship map.


### Function Node

A node usually refers to a message forwarding node, and there is no hard binding relationship with the account. An account can publish information through multiple nodes at the same time, and a node can also forward information from multiple accounts at the same time; a node can provide only a single spatiotemporal information, or it can provide multiple spatiotemporal information. Simply put, the node we are talking about is a three-party service that can provide messages in response to requests, similar to the DNS service in the Internet.

#### Time Proof Node

There will be multiple time certificate server nodes in the system, and the complete information of time certificates of multiple different flow rates can be stored on the nodes. The account can obtain the latest time certificate from the server and add it to its message. You can also obtain a historical time certificate of a certain time and space to verify the legitimacy of third-party information.

#### Account Information Node

Maintain the latest and most complete account information for one or more time and space, including legal account information, collect evil evidence of the account, etc., to help users improve the local account parent-source topology when receiving a message from an unknown source Illustration.

#### Account Status Node

Maintains the current status of the node, whether it is online, and listening port information, so that users can directly interact with each other in a P2P environment.

#### Message Distribution Node

Collect and maintain messages. Each message node determines the content of the message that it forwards (broadcasts) according to different subjective wishes (algorithms). A message node is equivalent to many websites on the Internet today. The difference is that the ownership of the message (content) is the message producer.


## World Creation Process

The process of creating and developing a PDU account system usually goes through the following steps:
1. Create the genesis file, which contains two public keys (Adam, Eve) and is considered to be the top of the account system topology diagram (DAG) of this PDU. The binary attributes of these two accounts must be different.
2. Create an initial N-generation account. During this process, Eve (also Adam) publishes time certification events. Adam and Eve and their sub-accounts within N generations, according to the time certification issued by Eve, are in line with the laws of nature. Under certain conditions, build a certain number of accounts.
3. Starting from a certain account in the above account, a stable time proof server is started to provide the initial time proof service in the P2P environment. This is the first time division of PDU. After that, users in the P2P environment can more easily participate in creating accounts.
4. The growth rate of the total number of accounts in the account system is controlled by the time proof. The slower the time flow rate, the slower the growth rate of the total number of accounts.
5. There are multiple proofs of different time flow rates, and there is a spatiotemporal split in the PDU. The user chooses a spatiotemporal space (which can meet multiple spatiotemporals at the same time) to create new accounts and use it.
6. Time and space coexist.

To be added ...

## Conclusion

In this paper, we propose a concept of a social network based on a decentralized account system. By orderly introducing time proof, all users on the P2P network are directly or indirectly given a cost. Users can choose their own network time and space according to their wishes. In this way, we return the user's identity and social relationship to the user itself, instead of having to rely on a particular three-party social network service.

Unlike the decentralized digital cryptocurrency represented by Bitcoin, PDUs do not use consensus to force the entire network to receive and maintain the only consistent data. Users can choose to receive the part of the entire network that is meaningful to them according to their own wishes. At the same time, it allows users to punish evil behaviors and disseminate evidence. Depending on the parental relationship of the DAG structure, association punishment can even be carried out, further increasing the cost of evil.

A known system is difficult to meet decentralization, efficiency and overall consistency at the same time. Because of the characteristics of the currency system, Bitcoin chose decentralization and consistency of the overall information. According to the characteristics of information transmission, PDU chose Decentralization and efficiency. We believe that in the process of information dissemination, a single node does not need to know all the complete information of the entire network in real time, and can tolerate the wrong information generated by the malicious behavior of an account.
