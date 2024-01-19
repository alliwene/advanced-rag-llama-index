# Notes

## Auto Merging Retrival

- In order to use an auto-version retriever, we need to parse our nodes in a hierarchical fashion.
- This means that nodes are parsed in decreasing sizes and contain relationships to their parent node.
- The way the index works is that we actually construct a vector index on specifically the leaf nodes.
- All other intermediate and parent nodes are stored in a doc store and are retrieved dynamically during retrieval.
- But what we actually fetch during the initial top $K$ embedding lookup is specifically the leaf nodes, and that's what we embed.
- The auto-merging retriever is what controls the merging logic.
- If a majority of children nodes are retrieved for a given parent, they are swapped out for the parent instead.
- In order for this merging to work well, we set a large top-k for the leaf nodes. And remember, the leaf nodes also have a smaller chunk size of 128.
- In order to reduce token usage, we apply a re-ranker after the merging has taken place.
