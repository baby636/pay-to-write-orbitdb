# pay-to-write-orbitdb

This started as an npm library and then grew into a Koa REST API server.
The reason it was converted was because the OrbitDB tries to validate each entry in the database on each startup of the software. The Mongo database is leveraged so that OrbitDB can quickly validate entries that it has already validated. So there are two code paths to validating datbase entries:

- The OrbitDB checks to see if the entry already exists in the MongoDB. If it does, the TXID (key) is considered valid. This case is optimized for fast start-up of this app.
- If the MongoDB does not have an entry for that TXID, then OrbitDB will validate the TXID by querying blockchain information through FullStack.cash. If validated, it will save the data to the MongoDB as well. This case is optimized for normal operation.

- [./old-lib/examples](./old-lib/examples) has some example scripts from the old library.

## Examples

- Read the README in the [Examples directory](./examples/README.md).

# Licence
[MIT](LICENSE.md)
