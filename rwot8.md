
# PSDAD - A new data format with secure semantics

## Abstract

Existing data serialization formats like JSON, JSON-LD, XML, and even
ASN.1 (with its various encoding rules) work well enough for
conventional computing environments, but they fall short when high
levels of both trust and decentralization are required. PSDAD
(plaintext self-describing assertional data) is a proposed new
approach which uses natural language strings simultaneously as
identifiers, delimiters, and documentation, resulting in a
surprisingly simple and robust system with distinct advantages over
all known current approaches in certain environments.  PSDAD has a
partial spec and partial implementation available.

## Motivation

Consider the scenario where machine Alice wants to send machine Bob a
machine-readable message, saying that some thermal probe (probe number
6) is currently reading 34C.

With **JSON**, she might encode it like this:

```json
{ 
  "probe": 6, 
  "temp": 34 
}
```

In this case, Bob can tell what she means -- like whether the
temperature is in Celsius or Fahrenheit -- by using external prior
agreements.  Perhaps they were at a hackathon together while building
this setup, or perhaps one or both of them is using software from a
vendor which has an available specification for its data format, and
somehow Alice and Bob have communicated they are both using that software.

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
https://alice.example/schema in a browser and perhaps finding some
useful information about the semantics of the data he has received.

One place these familiar techniques fall short is if there is confusion
about which definitions to use. That confusion might come from an
innocent mistake (such as poor communication during a schema migration), or it
might come from a disinformation attack, with someone deliberately
spreading misleading information about the semantics of Alice's data.

As long as Alice and Bob know each other, or are using the same
software, or are using data formats defined by large standards
organizations, the risk is probably small.  The risk becomes
significant, however, in a dynamic market around an open data bus,
with many different components and systems passing data around, with
increasingly complexity, and new formats appearing all the time.

Some people suggest the RDF (and XML) namespace architectures, as
shown above in JSON-LD, solve this problem because one can use the
namespace URL content as the master definition source. In theory this
could work, but in practice it has three problems:

1. The RDF specifications and current practice do not actually give
the namespace content any special privileged status. It is unclear
whether there is any way to add such special status after deployment.

2. This makes the namespace host a critical part of the
infrastructure. Now, when Alice and Bob communicate, they must also
trust the namespace host (thermal.example, in the above example). It
could make it significantly harder to build secure data communication
channels, and it increases the cost and liability for running a
namespace host.

3. Developing 




## Proposal

...
