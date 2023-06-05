# strapi-graphql

## Types

### User

- Description: Represents a post in the system.
- Fields:
  - `id` (ID): The unique identifier for the user.
  - `username` (String): The username of the user.
  - `email` (String): The email address of the user.
  - `createdAt` (String): The created at of the post.

### Post

- Description: Represents a post in the system.
- Fields:
  - `id` (ID): The unique identifier for the post.
  - `author` (User): The author of the post.
  - `title` (String): The title of the post.
  - `content` (String): The content of the post.
  - `createdAt` (DateTime): The date and time when the post was created.
  - `updatedAt` (DateTime): The date and time when the post was last updated.

### Comment

- Description: Represents a comment on a post.
- Fields:
  - `id` (ID): The unique identifier for the comment.
  - `text` (String): The content of the comment.
  - `author` (User): The author of the comment.
  - `createdAt` (DateTime): The date and time when the comment was created.
  - `updatedAt` (DateTime): The date and time when the comment was last updated.

### Like

- Description: Represents a like on a post.
- Fields:like
  - `id` (ID): The unique identifier for the like.
  - `post` (Post): The post of the like.
  - `user` (User): The user of the like.
  - `createdAt` (DateTime): The date and time when the like was created.

## Queries

### getPosts

- Description: Retrieves posts
- Return Type: Post

```graphql
query {
  posts {
    data {
      id
      attributes {
        title
        content
        thumbnail {
          data {
            id
            attributes {
              url
            }
          }
        }
        user {
          data {
            id
            attributes {
              username
              email
            }
          }
        }
      }
    }
  }
}
```

### getPostById

- Description: Retrieves a post by their ID.
- Arguments:
  - `id` (ID!): The ID of the post to retrieve.
- Return Type: Post

```graphql
query {
  post(id: 1) {
    data {
      id
      attributes {
        title
        content
        thumbnail {
          data {
            id
            attributes {
              url
            }
          }
        }
        user {
          data {
            id
            attributes {
              username
              email
            }
          }
        }
      }
    }
  }
}
```

### getPostComments

- Description: Retrieves the comments associated with a post.
- Arguments:
  - `postId` (ID!): The ID of the post to retrieve comments for.
- Return Type: [Comment]

```graphql
query {
  comments(filters: { post: { id: { eq: "6" } } }) {
    data {
      id
      attributes {
        content
        post {
          data {
            id
          }
        }
        author {
          data {
            id
            attributes {
              username
              email
            }
          }
        }
        createdAt
        updatedAt
      }
    }
  }
}
```

### getPostLikes

- Description: Retrieves the likes associated with a post.
- Arguments:
  - `postId` (ID!): The ID of the post to retrieve likes for.
- Return Type: [Like]

```graphql
query {
  likes(filters: { post: { id: { eq: "6" } } }) {
    data {
      id
      attributes {
        post {
          data {
            id
          }
        }
        user {
          data {
            id
            attributes {
              username
              email
            }
          }
        }
        createdAt
        updatedAt
      }
    }
  }
}
```

## Mutations

### createPost

- Description: Creates a new post.
- Arguments:
  - `title` (String!): The title of the post.
  - `content` (String!): The content of the post.
- Return Type: Post

```graphql
mutation createPost {
  createPost(data: { title: "Hello", content: "Hello", author: 1 }) {
    data {
      id
      attributes {
        title
        content
        author {
          data {
            id
            attributes {
              username
              email
            }
          }
        }
        createdAt
        updatedAt
      }
    }
  }
}
```

### updatePost

- Description: Updates an existing post.
- Arguments:
  - `id` (ID!): The ID of the post to update.
  - `title` (String!): The title of the post.
  - `content` (String!): The content of the post.
- Return Type: Post

```graphql
mutation {
  updatePost(
    id: 2
    data: { title: "Updated Post Title", content: "Updated post content." }
  ) {
    data {
      id
      attributes {
        title
        content
        author {
          data {
            id
            attributes {
              username
              email
            }
          }
        }
        createdAt
        updatedAt
      }
    }
  }
}
```

### deletePost

- Description: Deletes a post.
- Arguments:
  - `id` (ID!): The ID of the post to delete.
- Return Type: Post

```graphql
mutation {
  deletePost(id: 2) {
    data {
      id
    }
  }
}
```

### createComment

- Description: Creates a new comment.
- Arguments:
  - `content` (String!): The content of the comment.
- Return Type: Comment

```graphql
mutation createComment {
  createComment(data: { content: "Hello", author: 1 }) {
    data {
      id
      attributes {
        content
        post {
          data {
            id
          }
        }
        author {
          data {
            id
            attributes {
              username
              email
            }
          }
        }
        createdAt
        updatedAt
      }
    }
  }
}
```

### updateComment

- Description: Updates an existing comment.
- Arguments:
  - `id` (ID!): The ID of the comment to update.
  - `content` (String!): The content of the Comment.
- Return Type: Comment

```graphql
mutation {
  updateComment(id: 2, data: { content: "Updated comment content." }) {
    data {
      id
      attributes {
        content
        post {
          data {
            id
          }
        }
        author {
          data {
            id
            attributes {
              username
              email
            }
          }
        }
        createdAt
        updatedAt
      }
    }
  }
}
```

### deleteComment

- Description: Deletes a comment.
- Arguments:
  - `id` (ID!): The ID of the comment to delete.
- Return Type: Comment

```graphql
mutation {
  deleteComment(id: 2) {
    data {
      id
    }
  }
}
```

### createLike

- Description: Creates a new like for a post.
- Arguments:
  - `post` (ID!): The ID of the post to like.
  - `user` (ID!): The ID of the user who is liking the post.
- Return Type: Like

```graphql
mutation createLike {
  createLike(data: { post: 4, user: 2 }) {
    data {
      id
      attributes {
        post {
          data {
            id
          }
        }
        user {
          data {
            id
            attributes {
              username
              email
            }
          }
        }
        createdAt
      }
    }
  }
}
```

### deleteComment

- Description: Deletes a like.
- Arguments:
  - `id` (ID!): The ID of the like to delete.
- Return Type: Like

```graphql
mutation {
  deleteLike(id: 2) {
    data {
      id
    }
  }
}
```
