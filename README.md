RNS
===

Relational (or Relative) Name Service Model

If I know Julie, Mike and Bob, and Mike knows Fred Fredericksen and the other two know Fred Logan, and all 3 have related anecdotes to me about Fred without including his surname - or if I forget whose surname is whose - I understand Fred Fredericksen as "the Fred whom Mike knows" and Fred Logan as "the Fred whom Julie and Bob know" (assuming I know that Julie and Bob were talking about the same Fred). This is the basis for my relational name service model.



20140704	Relational Name Service part 2	Technical


Data field names and descriptors (probably use a backend database)

 Primary Name:		Name assigned by owner of table, for the purpose of referring to an entity's entire record

 Primary Number:		Numeric identifier paired with and for the same purpose as Primary Name
 
 Entity:			The self-identifier presented by this person at this connection (this field should be omitted in favor of Entities; I include it here to help the whole thing make better sense to the reader).
			An Entity's field contains its Origin, any Alias presented by the connection's requestor, and any information either peer sees fit to append to it. All information in an Entity field is appended into the field in the order in which it is first encountered.

 Credential:		A host-determined record containing at least the fields Origin and Password, plus whatever else a server (or a lower-level protocol) sees fit to require or accept in a given context. My own recommendation is 	{Origin[,Alias[,Identity]],Password[,PublicKey]}. Identity must default to Alias; Alias must default to Origin; PublicKey is a field used for verification of acceptibility in some of the protocols over which RNS should be capable of connecting. Note that placing Identity immediately before Password allows inclusion of Password within Identity, a very useful feature in some protocols.

 Origin:			The initial visible origin of a request to connect (IP or MAC or URL or referral or or or...)

 Password:		the passwords given by each Entity belonging to this Identity at connection (the Password field should be stored within the Credential field, being nearly useless outside of a Credential; even the order in which the fields of a Credential appear and the manner in which they are presented can be used in verification of identity)

 Identity:		Reference by Primary Name or Primary Number to the table containing the data for an Entity or Alias

 Aliases:			List of Aliases linked to this Identity. An Alias is a name given by an Entity for display to members of a set of people; the default set for an Alias comprises everyone except the hosting server and its admin; the latter see both each Entity, its Identity, and the Alias(es) under which it appears in (a) given context(s)

 Entities:		List of Entities linked to this Identity. An Entity is what each requestor for connection to this peer first appears as, with any identifying information encountered later (such as the name of a user of a public terminal) appended to it in the order in which each bit of information was encountered. The Identity field is searched before Entities during lookup, and should be where most information is stored.

 Keys:			A list of {name,value} pairs such as {"PublicKey","0f8h4f837g0v45wbf0sor8gvfo45w8ngpfw"} for use by other services with which RNS collaborates



Terms

Entity:		Someone who has requested connection to this peer

Identity:	Collection of Entities thought to be the same person

Alias:		Visible identifier chosen by an entity for view by a set of viewers

Points on the terms
- One Identity can refer to any number of Entities and vice versa
- One Entity or Identity can define any number of Aliases
- One Alias can refer to any number of Entities but only one Identity within a set; when more than one member of a set choose the same Alias, each is modified by the set by one of the following methods, at the discretion of the peer which hosts the table in which it is defined:
- - Append the ordinal of its occurrence to each Alias, as, Johnny1, Johnny2, Johnny3
- - Append a server timestamp to each Alias (deprecated in favor of the other methods because it offers no advantage at cost of some advantages, but retained in this model for backwards compatibility with certain IRC protocols)
- - Append the Origin (initial identifier of the Entity or Alias on first encounter by this peer), as, Johhny.25.122.3.25:443 (an appended IP address in this example)
- - Append the Referrer of each Entity to its name, as, Johnny.rnschat.www.freenode.net (RNS default naming scheme) or Johnny.www.freenode.net?#rnschat (example web-irc channel url -- no irc exists yet for relational name service models that I know of)
- - Append the Apparent-Origin (defined by the Entity to show other users what that Entity wants them to see), as, Johnny From RNSChat



--- This is only a draft of a model as of this writing. Updates when progress occurs. ---
