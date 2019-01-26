
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
machine-readible message, saying that some thermal probe (probe number
6) is currently reading 34C.

With **JSON**, she might encode it like this:

```json
{ 
  "probe": 6, 
  "temp": 34 
}
```

In this case, Bob can tell what she means -- like whether the
temperature is in Celcius or Farenheit -- by using external prior
agreements.  Perhaps they were at a hackathon together while building
this setup, or perhaps one or both of them is using software from a
vendor which has an available specification for its data format, and
somehow Alice and Bob have communicated they are both using that software.

With **JSON-LD**, Alice might encode her message like this:
```json
{
  "@context": {
    "probe": "https://alice.example/schema#probe",
    "temp": "https://alice.example/schema#temp"
  },
  "probe": 6, 
  "temp": 34 
}
```

Now Bob has the additional option of vising
https://alice.example/schema in a browser and perhaps finding some
useful information about the semantics of the data he has received.

One place these familiar techiques fall short is if there is confusion
about which definitions to use. That confusion might come from an
innoscent mistake (such as poor comminication during a schema migration), or it
might come from a disinformation attack, with someone deliberately
spreading misleading information about the semantics of Alice's data.






## Proposal

...
