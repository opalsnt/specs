![](https://img.shields.io/badge/status-wip-orange.svg?style=flat-square)

# Identity

-----

**Abstract**

Identities are use for verification and access control of database entries. They often contain keys used to digitally sign data and serve as a composable way to distribute access to multiple devices without sharing any private data.

# Table of Contents

- [Introduction](#introduction)
- [Formats](#Formats)
- [Validity](#validity)

## Introduction

Identities are used for entry validation and access control. Every entry will have or contain a reference to an identity.

## Formats

> List of spec'd identity formats

- [basal](./basal)

## Validity Constraints

An identity must pass all validity constraints of the identity format.
If one of these constaints is not satisfied the identity is invalid. Invalid identities cannot be added to the replica.


## Interface

The identity interface is defined:


###### see cbor [encoding specification](https://www.rfc-editor.org/rfc/rfc8949.html#name-specification-of-the-cbor-e) and [tag 42](https://github.com/ipld/cid-cbor/)

```
  {
    id: type 2
    auth: tag 42
  }
```

Identity formats do not need to match the interface at the encoding level. When decoded and verified by the identity format, this interface must be exposed.

The `id` field is a key used to control access. It does not need to be the signing key used by the identity. In most cases it will be a separate signing key used to sign other identities, giving them access under one identity id.

The `auth` field is the cid to the identity object. It is used in some entry formats as a reference to the identity, to deduplicate data.
