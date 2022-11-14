# GraphiQL Client
A simple ServiceNow GraphiQL implementation that allows you to make queries from within a tool within your instance.

Based on the https://github.com/graphql/graphiql repo, specifically the [CDN Example](https://github.com/graphql/graphiql/tree/main/examples/graphiql-cdn).

**Do Not Install on a Prod Instance--for Dev Use Only**

## Installation
1. Simply use source control to fork this repo and install that into your ServiceNow instance using Studio. 
2. Make sure that introspection is enabled at "System Web Services > GraphQL > Properties" (NOTE: DO THIS FOR DEV INSTANCES ONLY).  
3. Note: **turning on GlideRecord introspection** means that the *entire* schema of all your tables and fields will be downloaded. Needless to say this will take a couple of minutes each time the schema updates in the client.  If you are not using the GlideRecord_Query API you will want to leave this off, but luckily you only take this hit the first time you load the GraphQL client each day.

## Usage
Navigate to "System Web Services > GraphQL > GraphQL Explorer".

Available at the path:
/now/nav/ui/classic/params/target/x_snc_graphiql_gql.do

Type "{" then ctrl-space in the editor and you will see the available GraphQL Services auto complete.

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
