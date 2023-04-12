<div>

<div>

# GraphQL

</div>

<div>

## Prerequisites

<div>

<div>

-   Node.js

-   npm/yarn

</div>

</div>

</div>

<div>

## Installation

<div>

<div>

Use the following command to install the Neo4j GraphQL Library
dependencies using npm:

</div>

<div>

<div>

<div>

<div>

<div>

Copied!

</div>

</div>

</div>

    npm install @neo4j/graphql graphql apollo-server neo4j-driver

</div>

</div>

<div>

Use the following command to install the Neo4j GraphQL Library
dependencies using yarn:

</div>

<div>

<div>

<div>

<div>

<div>

Copied!

</div>

</div>

</div>

    yarn add @neo4j/graphql graphql apollo-server neo4j-driver

</div>

</div>

</div>

</div>

<div>

## Code example

<div>

<div>

<div>

<div>

<div>

<div>

Copied!

</div>

</div>

</div>

    const { Neo4jGraphQL } = require("@neo4j/graphql");
    const { ApolloServer, gql } = require("apollo-server");
    const neo4j = require("neo4j-driver");

    // (You may need to replace your connection details, username and password)
    const AURA_ENDPOINT = 'neo4j+s://<Bolt url for Neo4j Aura instance>';
    const USERNAME = '<Username for Neo4j Aura instance>';
    const PASSWORD = '<Password for Neo4j Aura instance>';

    // Create Neo4j driver instance
    const driver = neo4j.driver(AURA_ENDPOINT, neo4j.auth.basic(USERNAME, PASSWORD));

    const typeDefs = gql`
      type Person {
        name: String
        knows: [Person!]! @relationship(type: "KNOWS", direction: OUT)
        friendCount: Int @cypher(statement:"RETURN SIZE((this)-[:KNOWS]->(:Person))")
      }
    `;

    // Create instance that contains executable GraphQL schema from GraphQL type definitions
    const neo4jGraphQL = new Neo4jGraphQL({
      typeDefs,
      driver
    });

    // Generate GraphQL schema
    neo4jGraphQL.getSchema().then((schema) => {
      // Create ApolloServer instance to serve GraphQL schema
      const server = new ApolloServer({
        schema,
        context: { driverConfig: { database: 'neo4j' } }
      });

      // Start ApolloServer
      server.listen().then(({ url }) => {
        console.log(`GraphQL server ready at ${url}`);
      });
    })View all (24 more lines)

</div>

</div>

<div>

### Running the example

<div>

Follow the steps below to run the example code:

</div>

<div>

1.  Copy and paste the code above into a file named `example.js`.

2.  Enter the information for the AuraDB instance you want to connect to
    by replacing:

    <div>

    -   `<Bolt url for Neo4j Aura instance>` with the URI.

    -   `<Username for Neo4j Aura instance>` with the username.

    -   `<Password for Neo4j Aura instance>` with the password.

    </div>

3.  Use the following command to run the example code:

    <div>

    <div>

    <div>

    <div>

    <div>

    Copied!

    </div>

    </div>

    </div>

        node example.js

    </div>

    </div>

</div>

</div>

<div>

### Example walkthrough

<div>

You use the Neo4j GraphQL Library to create a GraphQL API backed by your
Neo4j Aura instance. The Neo4j GraphQL Library can generate a full
GraphQL API, including auto-generated data fetching logic from GraphQL
type definitions.

</div>

<div>

The example creates GraphQL type definitions to define the data model of
the API and the instance. It then passes these to the `Neo4jGraphQL`
class that contains an executable GraphQL schema object.

</div>

<div>

You then use Apollo Server to host the GraphQL schema. Once the GraphQL
server is running, navigate to localhost:4000 in your web browser to
query the GraphQL API using Apollo Studio.

</div>

</div>

<div>

### Querying with GraphQL

<div>

In GraphQL Playground, run the following mutation to create two Person
nodes, Alice and Dave, connected by a KNOWS relationship in the graph:

</div>

<div>

<div>

<div>

<div>

<div>

Copied!

</div>

</div>

</div>

    mutation {
      createPeople(
        input: [
          {
            name: "Alice"
            knows: { create: [{ name: "David" }] }
          }
        ]
      ) {
        people {
          name
          knows {
            name
          }
        }
      }
    }

</div>

</div>

<div>

Then you can query for the Person named Alice, and her friends:

</div>

<div>

<div>

<div>

<div>

<div>

Copied!

</div>

</div>

</div>

    query {
      people(where: { name: "Alice" }) {
        name
        friendCount
        knows {
          name
        }
      }
    }

</div>

</div>

</div>

</div>

</div>

<div>

## References

<div>

<div>

-   Neo4j GraphQL Library Documentation

-   GRANDstack blog

</div>

</div>

</div>

</div>
