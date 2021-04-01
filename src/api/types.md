# Types 

```json
{
  "Address": "AccountId",
  "LookupSource": "AccountId",
  "IdentityOf": {
    "id": "Hash"
  },
  "AuthorizedTokenOf": {
    "id": "Hash",
    "cost": "Balance",
    "data": "u64",
    "datatype": "u64",
    "expired": "u64"
  }
}
```

When using with Polkadot.js App you will need to add the above Litentry's types so it can encode and decode the extrinsic correctly, copy the following code to the text field on "developer" tabs: https://polkadot.js.org/apps//#/settings/developer .

![Example on Overwrite Types on Polkadot Apps](./useWithAPI.png)
