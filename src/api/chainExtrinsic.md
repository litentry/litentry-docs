# Extrinsic

#### issueToken

```rust,ignore
fn issueToken(to, identity_id, cost, data, datatype, expired)
```

Issue a token of an owned identity to certain account.

* `to`: Hash, the receiver identity id
* `identity_id`: Hash, the issuer identity id 
* `cost`: Balance, the transfer cost of the token
* `data`: byte, The data stored in the token
* `data_type`: byte, the type of the data represent in byte
* `expired`: byte, which define the expired date of the token

#### registerIdentity

```rust,ignore
fn registerIdentity()
```
Register a new identity for this account.

#### registerIdentityWithId

```rust,ignore
fn registerIdentityWithId(identity_id)
```

Register a new Identity with existed identifier as Identity ID, this is useful when register a third party devices or services. For example, a user buy a new IoT camera, there could already exist a identifier on the back of device reserved for the buyer.

* `identity_id`: Hash, the identifier to be used as identity ID

#### transferToken

```rust,ignore
fn transferToken(to, token_id)
```
Transfer a owned token to another account

* `to`: AccountId, the future owner of the token
* `token_id`: Hash, the ID of the transferred token
