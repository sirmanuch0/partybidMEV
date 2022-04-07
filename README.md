#Party Pooper

MEV on PartyBid

PartyBid is a protocol that allows users to pool their funds together to participate in an NFT auction. Anyone can contribute ETH to the PartyBid, and can trigger a bid from that party (which is always the minimum bid required to beat the next highest bidder).

A consequence of this mechanism is that the partybid can be forced to bid its full balance on the auction. This is a known mechanic of PartyBid, and was publicly disclosed in the project's security review.(https://hackmd.io/@alextowle/ryGQ4L-pd#PartyBid-Report)

Party Pooper is an implementation of this value extraction mechanism that leverages flash loans. The contract has a single external method raisePartyBid(address partyBid) that works as follows:

    Take out an aave flash loan
    Bid on auction
    Trigger a higher bid from partybid
    Return loan

This allows any third party to cause partybid to bid it's full balance on an auction. Credit to Frank.