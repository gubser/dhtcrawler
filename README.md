# dhtcrawler
Finds IP addresses and ports of BitTorrent clients by using the Distributed Hash Table (DHT).
Vast amounts of IP can be collected quickly and without actually torrenting anything. The collected clients are not part of a particular torrent, because the generated request sent by dhtcrawler is random.

## Method
To collect addresses, a DHT get_peers request with a random torrent infohash is sent to a peer. The communication happens over UDP and is stateless. The response packet contains a list of peers which, by protocol, contains either some peers currently serving the torrent or, if none are known, some peers which do probably know better about the requested torrent infohash. In either way, we add all peers to the list of known peers.
To increase the amount of peers collected from a peer, the get_peers request may be repeated with different torrent infohashes.

## Implementation
The crawler is implemented as a python generator. By the nature of the method, the output sequence may have repetitions.
