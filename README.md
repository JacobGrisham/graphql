# GraphQL with Node.js Backend

Below is code scaffolding. This is code that was originally in src/index.js and was used to achieve rudimentary features of graphql and to demonstrate what happens under the hood, particularly with Link resolver object.
```
const resolvers = {
  Query: {
    info: () => `This is the API of a Hackernews Clone`,
    feed: () => async (parent, args, context) => {
      return context.prisma.link.findMany()
    },
    get: (num) => { 
      let linkID = `link-${num}`
      let filtered = links.filter(function(link) { return link.num === linkID})
      let indexed = filtered[0]
      const link = {
        description: indexed.description,
        url: indexed.url,
      }
      return link
    }
  },
  Mutation: {
    post: (parent, args, context, info) => {
      const newLink = context.prisma.link.create({
        data: {
          url: args.url,
          description: args.description,
        },
      })
      return newLink
    }
  },
  // Don't need the following since it's so simple. GraphQL can infer this. It's good to know what's going on under the hood
  Link: {
    id: (parent) => parent.id,
    description: (parent) => parent.description,
    url: (parent) => parent.url,
  }
}
```