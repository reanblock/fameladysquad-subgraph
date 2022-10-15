# Subgraph Example using fameladysquad NFT

Below are basic steps taken to develop, build and deploy the [jensendarren/fameladysquad](https://thegraph.com/hosted-service/subgraph/jensendarren/fameladysquad) subgraph.

## Development

To develop a subgraph, follow these steps. 

1. Open [Hosted Service](https://thegraph.com/hosted-service) and sign up with your Github handle.
1. Navigate to **My Dashboard**, then press **Add subgraph**. Supply a name and description for your subgraph.
1. Install The Graph CLI with this command: `npm install -g @graphprotocol/graph-cli` (**NOTE**: Recommmend using Node 16)
1. Initialize your subgraph via the CLI command:`graph init --from-contract 0xf3E6DbBE461C6fa492CeA7Cb1f5C5eA660EB1B47 \ --contract-name Token --index-events` 
1. In your [schema.graphql](./schema.graphql) file, define your schema using the GraphQL interface definition language.
1. Generate some code using `graph codegen` which generates the code in the [generated](./generated/) directory.
1. In the [subgraph.yaml](./subgraph.yaml) file, you can now define the:
    1. The events you want to listen for under `dataSources.mapping.eventHandlers` 
    1. The [Starting Block](https://etherscan.io/tx/0xe4da13e944627e37ca8e5a2b78bda490bce02902cb706eb3976fa6b9e6cc00b0) for which the indexer should start indexing under `dataSources.source.startBlock`
    1. The names of the entities you want to query information about under `dataSources.mapping.entities`
1. Finally, write [mappings](./src/mapping.ts) in AssemblyScript which transforms the raw Ethereum data read from the blockchain into the entities defined in your schema.

## Build & Deploy

To build and deploy:

1. Run `graph build` to build your subgraph which generates the build under [build](./build/) directory.
1. Now authenticate your local graph cli with the hosted service using `graph auth --product hosted-service <ACCESS_TOKEN>`
1. Deploy your subgraph using `yarn deploy`
1. Check your subgraph in the Hosted Service Dashboard. In this case it is located at [https://thegraph.com/hosted-service/subgraph/jensendarren/fameladysquad](https://thegraph.com/hosted-service/subgraph/jensendarren/fameladysquad)
1. Query the new subgraph. In the case of this workshop the query endpoint is: [https://api.thegraph.com/subgraphs/name/jensendarren/fameladysquad](https://api.thegraph.com/subgraphs/name/jensendarren/fameladysquad)

## Note

As of subgraph spec version `0.0.4`, you need to declare all the features you're using, in the manifest section of [subgraph.yaml](./subgraph.yaml). For example, I added the following to the `subgraph.yaml` file to be able to deploy:

```
features:
  - ipfsOnEthereumContracts
```

### References

For more detail, please referr to [camiinthisthang/thegraph-workshop](https://github.com/camiinthisthang/thegraph-workshop/blob/main/README.md) which is the exercise I followed to create this subgraph.