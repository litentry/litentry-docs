# Chain State Storage

#### Identity Related

```rust,ignore
Identities: T::Hash => IdentityOf<T>;
IdentityOwner: T::Hash => Option<T::AccountId>;

IdentitiesCount: u64;
IdentitiesArray: u64 => T::Hash;
IdentitiesIndex: T::Hash => u64;

OwnedIdentitiesCount: T::AccountId => u64;
OwnedIdentitiesArray: (T::AccountId, u64) => T::Hash;
OwnedIdentitiesIndex: T::Hash => u64;
```

#### Token Related

```rust,ignore
AuthorizedTokens: T::Hash => AuthorizedTokenOf<T>;
AuthorizedTokenOwner: T::Hash => Option<T::AccountId>;
AuthorizedTokenIdentity: T::Hash => Option<T::Hash>;

AuthorizedTokensCount: u64;
AuthorizedTokensArray: u64 => T::Hash;
AuthorizedTokensIndex: T::Hash => u64;

OwnedAuthorizedTokensCount: T::AccountId => u64;
OwnedAuthorizedTokensArray: (T::AccountId, u64) => T::Hash;
OwnedAuthorizedTokensIndex: T::Hash => u64;

IdentityAuthorizedTokensCount: T::Hash => u64;
IdentityAuthorizedTokensArray: (T::Hash, u64) => T::Hash;
IdentityAuthorizedTokensIndex: T::Hash => u64;
```
