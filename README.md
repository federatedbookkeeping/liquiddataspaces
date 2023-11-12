# liquiddata
Thoughts on Liquid Data

## Layer 1
### authorities
### legal contract
## Layer 2
### access control
### theory of network
### logging requirements 
## Layer 3
### requirement models
### consent languages 
## Layer 4
### transport
## Layer 5
### Basics
### inception
### change
## Layer 6
### LRI matching 
## Layer 7
### agreement
### listening
## Layer 8
### theory of mind
### reasoning
### evolution
## Layer 9
### translation
### lookalike sets
### exhaustive lists
### negative statements 
## Layer 10
### CRDT
### blockchain
### write access 
## Layer 11
### contradiction
### conflict resolution 
## Layer 12
### audit

Theory of network:
It should be clear from the ruleset codified in the legal framework which authorities are allowed to read which quints when and under which conditions.
Also: keeping a copy, for how long, and various ways of using that copy, audit requirements.
End-users are also authorities. It’s up to each authority to codify all legal requirements in such a way that no mistakes are made, but requirements will often be contingent on machine readable instructions. We leave those at a higher layer though 


Basics:
Statements and assets.
Assets are content-addressable
Statements are quads where the why is the authority making the statement.
Maybe quints if we add a timestamp.

Subject and predicate URIs are relative to the authority. We call them LRIs for that reason.
Object is either a literal or an LRI relative to the authority.
Literals can be very large so we call them assets.

LRI matching:
Matchers translate the LRIs between authorities. They are append-only Last Write Wins lists of quints where the predicate is ‘matches’.

If there is no 1-1 mapping between remote and local LRIs, mint local ones until there is. This could be as easy as using the remote authority ID as a prefix. But that does mean those prefixes will concatenate for multihop 

Non-repudiability and tamper proofing:
Each authority signs their statements.

Change:
The meaning of an LRI is immutable although it’s meaning can be a thing that in the outside world changes over time.

Access control:
When syncing data, make it clear what the audience of the payload is. We need a language for that.
Minimise the number of systems that get a copy of the data, given the users that need access to it. We need language to describe that principle in more detail, e.g. break glass access etc.

Legal basis:
Sign legal contracts about remote enforcement of access control (including NDA), SLA, conflict resolution, copyright (especially of assets), etc.
Certain LRIs can also take on legal meaning, for instance “I owe you”

Agreement:
Through the application of matchers (single hop or multihop), systems can conclude that they agree with the latest info received from a neighbour.

Transport:
Could be several things, for instance Merckle trees. Assets might be stored in separate key-value stores such as DHTs. Sync messages should probably be timestamped, signed and chained to make data leaks auditable. Maybe the receiver should then also sign the timestamp of receiving. Or silence should be timestamped to prevent backdating. Details TBD.

You can use abbreviated formats such as csv that could be interpreted (but not necessarily in one unique way) as quints from the context

Inception:
Each quint automatically is an asset. That way you can chain replies etc.

Evolution:
Sometimes matchers are not enough.
LRIs can split and merge. We need a language to express how LRIs evolve over time.

Translation:
Sometimes there will be translation processes that are easier to describe procedurally than in terms of LRI matching + reasoning. For instance, if I organise my addressbook in one file per group and you have one big list, then we need shuffle things around whenever data comes in. Don’t impose a quint store on people! 

Theory of Mind:
Each authority has one single own truth about the outside world, but it can describe the thoughts of others (as well as things it is not sure about) using quint assets.

Listening:
Just like when you merge changes from a remote repo, you can adopt statements from other authorities as your own.

Reasoning:
You can draw conclusions that basically combine knowledge into new statements.
You can also reason about your own previous quints.

CRDTs:
In particular, you can evolve assets to incorporate knowledge that comes in quints.

Blockchain:
You can use a consensus algorithm (Proof of Work or otherwise) that reasons about statements from various authorities with the goal of agreeing on a unanimous view of the outside world 

Write access:
Writing outside your own authority is impossible but we need a language to express expectations for the listening/reasoning other authorities will do. This can also be added to the legal contract.

Contradiction:
Last Write Wins but quints that have the same timestamp still cause contradiction. Also, contradiction may be subtle. For instance, if the conclusion of reasoning from two statements suggests I was bigger than a house, it should raise an alarm bell even though our model of the world may not strictly rule it out. Not sure how to deal with this. Rulesets? How do Gaia-X rulesets work?

…:
Anything else?
