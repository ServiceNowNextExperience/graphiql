# GraphiQL Client
A simple client side GraphiQL implementation that allows you to make queries from within the tool.

Based on the https://github.com/graphql/graphiql repo, specifically the [CDN Example](https://github.com/graphql/graphiql/tree/main/examples/graphiql-cdn).

Simply use source control to install this in your ServiceNow instance and make sure that introspection is enabled at "System Web Services > GraphQL > Properties".  Note: turning on GlideRecord introspection means that the entire schema of all your tables will be downloaded which will take a couple of minutes each time the schema updates in the client.

Then navigate to "System Web Services > GraphQL > GraphQL Explorer".

Type "{" then ctrl-space in the editor and you will see the available GraphQL Services.

Sample query:

```
query ($limit: Int = 5) {
  GlideRecord_Query {
    incident(queryConditions: "active=true", pagination: {limit: $limit}) {
      _rowCount
      _results {
        short_description {
          value
        }
        sys_id {
          value
        }
        state {
          value
          displayValue
        }
      }
    }
  }
}
```
