
# PSDAD - A new data format with secure semantics

Submission to: [Rebooting the Web of Trust #8](https://github.com/WebOfTrustInfo/rwot8-barcelona) (March 2019, Barcelona)

Author: [Sandro Hawke](https://www.w3.org/People/Sandro) < sandro@w3.org >

## Abstract

Existing data serialization formats like JSON, JSON-LD, XML, and even
ASN.1 (with its various encoding rules) work well enough for
conventional computing environments, but they fall short when high
levels of both trust and decentralization are required. PSDAD
(plaintext self-describing assertional data) is a proposed new
approach which uses natural language strings simultaneously as
identifiers, delimiters, and documentation, resulting in a
surprisingly simple and robust system with distinct advantages over
known approaches in certain environments.  PSDAD has a [partial
spec](https://sandhawke.github.io/psdad/spec.html) and [partial
implementation](https://github.com/sandhawke/psdad.js) available.

## Motivation

Consider the scenario where Alice wants to send Bob a machine-readable
message saying that some thermal probe (probe number 6) is currently
reading 34°C.  With **JSON**, she might encode it like this:

```json
{ 
  "probe": 6, 
  "temp": 34 
}
```

To properly understand this message, Bob needs to know its syntax and
semantics. In particular, how can he tell whether the temperature is in
Celsius, Fahrenheit, Kelvin, or some application-specific scale?

This has to be communicated out-of-band, via external means.  Perhaps
Alice and Bob were at a hackathon together while building this system.
Or maybe Alice wrote a blog post about it, which Bob found via search
engine.  Or maybe the data is being sent to a reserved and
[registered](https://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml)
port, so it's clear which RFC defines the temperature scale.  Or,
perhaps most commonly, maybe Alice and Bob are both using the same
software, and it uses some hardcoded [unofficial
port](https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers)
to talk to what it presumes are other instances of itself.

With **JSON-LD**, Alice might encode her message like this:
```json
{
  "@context": {
    "probe": "https://thermals.example/schema#probe",
    "temp": "https://thermals.example/schema#temp"
  },
  "probe": 6, 
  "temp": 34 
}
```

Now Bob has the additional option of visiting
https://thermals.example/schema in a browser and perhaps finding some
useful information about the semantics of the data he has received.

One place these familiar techniques fall short is if there is
confusion about which definitions to use. That confusion might come
from an innocent mistake (such as poor coordination during schema
evolution), or it might come from a disinformation attack, with
someone deliberately spreading misleading information about the
semantics of Alice's data.

As long as Alice and Bob know each other, are using the same software,
or are using data formats defined by large standards organizations,
the risk is probably small.  The risk becomes significant, however, in
a dynamic market around an open data bus (such as the web), with many
different components and systems passing data around, with
increasingly complexity, and new formats or extensions appearing over
time.

Some people suggest the RDF (and XML) namespace architectures, as
shown above in JSON-LD, solve this problem because one can use the
namespace URL content as the master definition source. In theory this
could work, but in practice it has three problems:

1. The W3C RDF specifications and current practice do not actually
give the namespace content any special privileged status. If the
content disagrees with search engine results or word-of-mouth, it's
unclear which should be taken as correct. It is also unclear whether
there is any way to add such special status now, long after the spec
have been published.

2. This makes the namespace host a part of the critical security
infrastructure. Now, when Alice and Bob communicate, they must also
trust the namespace host (thermal.example, in the above example). It
could make it significantly harder to build secure data communication
channels, and it increases the cost and liability for running a
namespace host. Arguable, it increases centralization around major
namespaces.

3. Not everybody is willing to use RDF, even in the form of JSON-LD.

The author observes these concerns becoming more pressing as the
[Credible Web Community Group](https://credweb.org) moves toward
creating a data ecosystem to help combat online misinformation. There
may be others in the larger community with similar concerns.

## Alternatives

The author is not aware of anyone else having done work on this
problem. He himself has developed another solution which applies only
to the RDF space, [Movable Schemas](https://sandhawke.github.io/mov/),
possibly with
[version-integrity](https://github.com/sandhawke/version-integrity). PSDAD
is the extension of Movable Schemas idea to the larger field beyond RDF.

## Proposal

PSDAD starts with the observation that the semantics of each field in
a data format are in practice defined by a short
paragraph in some specification. For example:

...

Then we ask: why go to great effort to connect a field securely to
that text in some remote document, when we can just put the text and
the field together in the instance data?

So, in practice, ...

...
