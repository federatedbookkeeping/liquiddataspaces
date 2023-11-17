# Liquid Data
### *a pluggable framework for data portability*

## Framing
Data portability requires trust. Most Chief Information Officers (CIOs) are rightfully conservative in allowing data to enter and leave the firewalls of their organisations. At the same time, if data is allowed to flow to the right place in an automated way, all parties involved, and the economy as whole, gains a lot of efficiency and additional value production. It is therefore really great that the EU sponsors open source data portability technology projects with hundreds of millions of euros through programs such as Smart Middleware Platform for Cloud-to-Edge Federations (SiMPL) and Next Generation Internet (NGI). Our challenge as technologists is to offer the European economy the best possible open source technology in return for this generous funding.

In order to build good data portability tools, we need to start with a good model of the landscape in which these tools will operate, to describe the current situation and contrast it with the desired situation, to see which tools could help us get there. The Liquid Data Framework therefore consists of a baseline model (describing the context in which data portability tools operate), a set of functional components that are defined in terms of their requirements, and a set of pluggable implementations of such components.

## Liquid Data Principles
1) **Federation** (Authorities and Communication): We model the world as a number of authorities, connected through neighbour-to-neighbour messaging connections (for instance REST APIs from which information can be pulled, or WebSockets through which information can be pushed). There is no central point in this network - the architecture is similar to that of the internet itself.

2) **Technical Sovereignty**: Each authority is entirely sovereign in how they design their internal database and how they operate it.

3) **Heterogenious Connections**: We reject tools that require a technological monoculture in order to achieve their value. This is similar to principle 2, but applied to the connections instead of to the internals of each authorities.

4) **Talk about the World** (Statements and Assets): A statement says something about the outside world and can be false. An asset is valuable in itself, for instance a drawing. Statements can refer to assets and to other statements Assets can contain representations of statements and other assets. You never know for sure if a statement is true.

5) **Local Resource Identifiers**: We do not impose any particular way of assigning identifiers when serialising statements into assets. This means that the sender's identifiers will have to be mapped onto the receiver's identifiers, and the case where both sender and receiver use the same URL for the same object is considered a coincidence. This also follows from princples 2 and 3.

## The rest of this is mainly random notes, still to be organised:

Authorities
We start by defining the organisational entities that use data as 'authorities'. An authority is any system that can hold information - so it can be a company, a hospital, a national chamber of commerce, a smart phone, or a human being. We 

• authorities (apps, services, users, governments, ...)
• APIs (REST, WebSocket, emails with PDFs, eDelivery) 
• legal contracts (various jurisdictions, ToS;DR, smart contracts)
• {assets, statements} containing {assets, statements} (RDF, git branches)
• "the machines knows what the other machines mean" (translation, LRI mapping)
• latency, manual data entry
• which data is allowed to go where? - multihop
• technical sovereignty

Problem statement: 
Someone would benefit if data would flow through the APIs of authorities.
One-of integrations are expensive, we can gain from repeatable know-how.

Examples:
LRI mapping in Federated Timesheets
Union data formats

---

spectrum from walled garden to public ledger

---


Assumptions:
federation
technical sovereignty
heterogeneous network
LRIs
multiple views on the outside world

---

why not PKI instead of a public ledger?

could you create a crypto currency based on VC and PKI? you need global consensus

## Layer 1
### authorities
### legal contract
Sign legal contracts about remote enforcement of access control (including NDA), SLA, conflict resolution, copyright (especially of assets), etc.
Certain LRIs can also take on legal meaning, for instance “I owe you”


## Layer 2
### access control
When syncing data, make it clear what the audience of the payload is. We need a language for that.
Minimise the number of systems that get a copy of the data, given the users that need access to it. We need language to describe that principle in more detail, e.g. break glass access etc.

### theory of network
It should be clear from the ruleset codified in the legal framework which authorities are allowed to read which quints when and under which conditions.
Also: keeping a copy, for how long, and various ways of using that copy, audit requirements.
End-users are also authorities. It’s up to each authority to codify all legal requirements in such a way that no mistakes are made, but requirements will often be contingent on machine readable instructions. We leave those at a higher layer though 

### logging requirements 
## Layer 3
### requirement models
### consent languages 
## Layer 4
### transport
Could be several things, for instance Merckle trees. Assets might be stored in separate key-value stores such as DHTs. Sync messages should probably be timestamped, signed and chained to make data leaks auditable. Maybe the receiver should then also sign the timestamp of receiving. Or silence should be timestamped to prevent backdating. Details TBD.

You can use abbreviated formats such as csv that could be interpreted (but not necessarily in one unique way) as quints from the context

## Layer 5
### Basics
Statements and assets.
Assets are content-addressable
Statements are quads where the why is the authority making the statement.
Maybe quints if we add a timestamp.

Subject and predicate URIs are relative to the authority. We call them LRIs for that reason.
Object is either a literal or an LRI relative to the authority.
Literals can be very large so we call them assets.

### inception
Each quint automatically is an asset. That way you can chain replies etc.

### change
The meaning of an LRI is immutable although it’s meaning can be a thing that in the outside world changes over time.

## Layer 6
### LRI matching
Matchers translate the LRIs between authorities. They are append-only Last Write Wins lists of quints where the predicate is ‘matches’.

If there is no 1-1 mapping between remote and local LRIs, mint local ones until there is. This could be as easy as using the remote authority ID as a prefix. But that does mean those prefixes will concatenate for multihop 

Non-repudiability and tamper proofing:
Each authority signs their statements.

## Layer 7
### agreement
Through the application of matchers (single hop or multihop), systems can conclude that they agree with the latest info received from a neighbour.

### listening
Just like when you merge changes from a remote repo, you can adopt statements from other authorities as your own.

## Layer 8
### theory of mind
Each authority has one single own truth about the outside world, but it can describe the thoughts of others (as well as things it is not sure about) using quint assets.

### reasoning
You can draw conclusions that basically combine knowledge into new statements.
You can also reason about your own previous quints.

### evolution
Sometimes matchers are not enough.
LRIs can split and merge. We need a language to express how LRIs evolve over time.

## Layer 9
### translation
Sometimes there will be translation processes that are easier to describe procedurally than in terms of LRI matching + reasoning. For instance, if I organise my addressbook in one file per group and you have one big list, then we need shuffle things around whenever data comes in. Don’t impose a quint store on people! 


### lookalike sets
### exhaustive lists
### negative statements 
## Layer 10
### CRDT
In particular, you can evolve assets to incorporate knowledge that comes in quints.

### blockchain
You can use a consensus algorithm (Proof of Work or otherwise) that reasons about statements from various authorities with the goal of agreeing on a unanimous view of the outside world 

### write access
Writing outside your own authority is impossible but we need a language to express expectations for the listening/reasoning other authorities will do. This can also be added to the legal contract.

## Layer 11
### contradiction
Last Write Wins but quints that have the same timestamp still cause contradiction. Also, contradiction may be subtle. For instance, if the conclusion of reasoning from two statements suggests I was bigger than a house, it should raise an alarm bell even though our model of the world may not strictly rule it out. Not sure how to deal with this. Rulesets? How do Gaia-X rulesets work?

### conflict resolution 
## Layer 12
### audit
