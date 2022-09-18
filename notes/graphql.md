# GRAPHQL

## Description

It's a query language that can be used by client and api to exchange informations.

## Main Features

1. Developers obtain only what they have requested, responses are always predicable.

```graphql
{
  hero {
    name
    height

  }
}
```

```json
{
  "hero": {
      "name": "Luke Skywalker",
      "height": 1.72
  }
}
```

2. Request more than one resource with a single query.

```graphql
{
  hero {
    name
    friends {
      name
      species {
        name
      }
    }
  }
}
```

3. Graphql apis and client share common strict type structures.


## Query Examples

```graphql
query fetchUsersById($id: ID = 1) {
  user(id: $id) {
    id
    name
    email
  }
}

query fetchUsersByOptions($options: PageQueryOptions!) {
  users(options: $options) {
    data {
      id
      name
      email
    }
  }
}
```

## Mutation examples

```graphql
mutation CreateReviewForEpisode($ep: Episode!, $review: ReviewInput!) {
  createReview(episode: $ep, review: $review) {
    stars
    commentary
  }
}
```
