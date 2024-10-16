# pay-to-write-orbitdb

This started as an npm library and then grew into a Koa REST API server.
The reason it was converted was because the OrbitDB tries to validate each entry in the database on each startup of the software. The Mongo database is leveraged so that OrbitDB can quickly validate entries that it has already validated. So there are two code paths to validating datbase entries:

- The OrbitDB checks to see if the entry already exists in the MongoDB. If it does, the TXID (key) is considered valid. This case is optimized for fast start-up of this app.
- If the MongoDB does not have an entry for that TXID, then OrbitDB will validate the TXID by querying blockchain information through FullStack.cash. If validated, it will save the data to the MongoDB as well. This case is optimized for normal operation.

- [./old-lib/examples](./old-lib/examples) has some example scripts from the old library.

## Next Steps

The following improvements need to be made to this code base:

- Create `_validateSignature()` function in TODO in [pay-to-write-access-controller.js](./src/lib/orbitdb/pay-to-write-access-controller.js).
- Capture signature in `writeToDb()` in API controller.
- Add unit tests
- Port code to an [ipfs-service-provider](https://github.com/Permissionless-Software-Foundation/ipfs-service-provider), and recreate the same REST API functionality with the JSON RPC.
- Add API calls for basic wallet functionality over both REST API and JSON RPC.
- Fork [gatsby-ipfs-web-wallet](https://github.com/Permissionless-Software-Foundation/gatsby-ipfs-web-wallet) and modify so that it can work off the REST API or IPFS JSON RPC functionality of the server.
  - Package the front end and back end in the same repository.

# Licence
[MIT](LICENSE.md)
