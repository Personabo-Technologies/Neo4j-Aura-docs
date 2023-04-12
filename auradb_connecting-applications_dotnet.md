<div>

<div>

# .NET

</div>

<div>

## Prerequisites

<div>

<div>

-   .NET SDK (Core)

</div>

</div>

</div>

<div>

## Installation

<div>

<div>

1.  Use the following command to create a new project:

    <div>

    <div>

    <div>

    <div>

    <div>

    Copied!

    </div>

    </div>

    </div>

        dotnet new console -o Neo4jAuraExample

    </div>

    </div>

2.  Navigate into the newly created directory:

    <div>

    <div>

    <div>

    <div>

    <div>

    Copied!

    </div>

    </div>

    </div>

        cd Neo4jAuraExample

    </div>

    </div>

3.  Install the .NET Driver using Package Manager:

    <div>

    <div>

    <div>

    <div>

    <div>

    Copied!

    </div>

    </div>

    </div>

        dotnet add package Neo4j.Driver

    </div>

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

    using Neo4j.Driver;
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Threading.Tasks;

    public class DriverIntroductionExample : IDisposable
    {
        private bool _disposed = false;
        private readonly IDriver _driver;

        ~DriverIntroductionExample() => Dispose(false);

        public DriverIntroductionExample(string uri, string user, string password)
        {
            _driver = GraphDatabase.Driver(uri, AuthTokens.Basic(user, password));
        }

        public async Task CreateFriendship(string person1Name, string person2Name)
        {
            // To learn more about the Cypher syntax, see https://neo4j.com/docs/cypher-manual/current/
            // The Reference Card is also a good resource for keywords https://neo4j.com/docs/cypher-refcard/current/
            var query = @"
            MERGE (p1:Person { name: $person1Name })
            MERGE (p2:Person { name: $person2Name })
            MERGE (p1)-[:KNOWS]->(p2)
            RETURN p1, p2";

            await using var session = _driver.AsyncSession(configBuilder => configBuilder.WithDatabase("neo4j"));
            try
            {
                // Write transactions allow the driver to handle retries and transient error
                var writeResults = await session.ExecuteWriteAsync(async tx =>
                {
                    var result = await tx.RunAsync(query, new { person1Name, person2Name });
                    return await result.ToListAsync();
                });

                foreach (var result in writeResults)
                {
                    var person1 = result["p1"].As<INode>().Properties["name"];
                    var person2 = result["p2"].As<INode>().Properties["name"];
                    Console.WriteLine($"Created friendship between: {person1}, {person2}");
                }
            }
            // Capture any errors along with the query and data for traceability
            catch (Neo4jException ex)
            {
                Console.WriteLine($"{query} - {ex}");
                throw;
            }
        }

        public async Task FindPerson(string personName)
        {
            var query = @"
            MATCH (p:Person)
            WHERE p.name = $name
            RETURN p.name";

            await using var session = _driver.AsyncSession(configBuilder => configBuilder.WithDatabase("neo4j"));
            try
            {
                var readResults = await session.ExecuteReadAsync(async tx =>
                {
                    var result = await tx.RunAsync(query, new { name = personName });
                    return await result.ToListAsync();
                });

                foreach (var result in readResults)
                {
                    Console.WriteLine($"Found person: {result["p.name"].As<String>()}");
                }
            }
            // Capture any errors along with the query and data for traceability
            catch (Neo4jException ex)
            {
                Console.WriteLine($"{query} - {ex}");
                throw;
            }
        }

        public void Dispose()
        {
            Dispose(true);
            GC.SuppressFinalize(this);
        }

        protected virtual void Dispose(bool disposing)
        {
            if (_disposed)
                return;

            if (disposing)
            {
                _driver?.Dispose();
            }

            _disposed = true;
        }

        public static async Task Main(string[] args)
        {
            // Aura queries use an encrypted connection using the "neo4j+s" protocol
            var uri = "neo4j+s://<Bolt url for Neo4j Aura instance>";
            var user = "<Username for Neo4j Aura instance>";
            var password = "<Password for Neo4j Aura instance>";

            using var example = new DriverIntroductionExample(uri, user, password);
            await example.CreateFriendship("Alice", "David");
            await example.FindPerson("Alice");
        }
    }View all (98 more lines)

</div>

</div>

<div>

### Running the example

<div>

Follow the steps below to run the example code:

</div>

<div>

1.  Copy and paste the code above into a file named `Program.cs`.

2.  Enter the information for the AuraDB instance you want to connect to
    by replacing:

    <div>

    -   `<Bolt url for Neo4j Aura instance>` with the URI.

    -   `<Username for Neo4j Aura instance>` with the username.

    -   `<Password for Neo4j Aura instance>` with the password.

    </div>

3.  Use the following command to generate an executable:

    <div>

    <div>

    <div>

    <div>

    <div>

    Copied!

    </div>

    </div>

    </div>

        dotnet build

    </div>

    </div>

4.  Use the following command to run the example code:

    <div>

    <div>

    <div>

    <div>

    <div>

    Copied!

    </div>

    </div>

    </div>

        dotnet run

    </div>

    </div>

</div>

</div>

<div>

### Example walkthrough

<div>

The example imports `Neo4j.Driver` to connect to the Neo4j AuraDB
instance.

</div>

<div>

The `Main` function calls the following two functions:

</div>

<div>

-   `CreateFriendship` creates two \'Person\' nodes, Alice and David,
    and a \'KNOWS\' relationship between them using a write transaction.

-   `FindPerson` finds Alice using a read transaction.

</div>

<div>

<div>

<table>
<tbody><tr>
<td>
<i></i>
</td>
<td>
<div>
<p>Developing with Neo4j Aura requires the use of <a>Transaction Functions</a>. Transaction Functions enable automatic recovery from transient network errors and enable load balancing.</p>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

<div>

Make sure to log queries and data sent from your application as it is
useful when you encounter errors and can help with debugging. This
example catches a `Neo4jException`.

</div>

</div>

</div>

</div>

<div>

## References

<div>

<div>

-   Neo4j .NET Driver Documentation

</div>

</div>

</div>

</div>
