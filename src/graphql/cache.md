# Middleware

[API of data server](dataServer.md)

Live Server: [https://graphql.litentry.com:4000/playground](https://graphql.litentry.com:4000/playground)

Github Repository: [https://github.com/litentry/litentry-ipfs-graphql](https://github.com/litentry/litentry-ipfs-graphql)

Currently, we provide a GraphQL caching server for recording event on the Litentry blockchain and caching data from IPFS.

IPFS is still under testing, graphql caching server could improve user experience for sync the data, it also caching anonymous data, and improve data query speed. 

![Graphql Server](./graphql1.png)

Query types

```typescript
  type Record {
    ${recordKey}: String
  }

  type Query {
    registerIdentity(identityId: String): String
    determineAddress(identityId: String): String
    addData(identityId: String, data: String): String
    addDataAddress(address: String, data: String): String
    getData(identityId: String): [Record]
  }
```

Example for query `playgroundRecord` data of certain identity  

```
https://graphql.litentry.com:4000/graphql?query={getData(identityId:"0x992c710c7fba11ccd22a2fbfec1af6ea85d488807e63e10cbbd16256fcf95752"){playgroundRecord}}
```

query IPFS address of certain identity
```
https://graphql.litentry.com:4000/graphql?query={determineAddress(identityId:"0x992c710c7fba11ccd22a2fbfec1af6ea85d488807e63e10cbbd16256fcf95752")}
```

