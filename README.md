# Prisma playground

* Clone this repo
* Run `npm install`
* Run `npm run dev` to start the graphql playground

- And execute the following query. The `notPublished` and `publishedPosts` returns null.

```
{
  usersGroupedPosts {
    name
    notPublished: posts(where: {
      isPublished: false
    }) {
      title
    }
    publishedPosts: posts(where: {
      isPublished: true
    }) {
      title
    }
  }
}
```

#### Actual

```
{
  "data": {
    "usersGroupedPosts": [
      {
        "name": "Vimal",
        "notPublished": null,
        "publishedPosts": null
      },
      {
        "name": "Bhuvana",
        "notPublished": null,
        "publishedPosts": null
      }
    ]
  }
}
```

#### Expected

```
{
  "data": {
    "usersGroupedPosts": [
      {
        "name": "Vimal",
        "notPublished": [],
        "publishedPosts": [
          {
            "title": "Some title"
          }
        ]
      },
      {
        "name": "Bhuvana",
        "notPublished": [
          {
            "title": "Pending title"
          }
        ],
        "publishedPosts": [
          {
            "title": "New title"
          }
        ]
      }
    ]
  }
}
```
