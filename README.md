# Personal Website

This was built with Vue 3 and uses the Contentful GraphQL API to fetch content.

The live version is deployed at: www.marisali.com

## Running locally

In order to fetch content from Contentful, create an `.env` file and add the following environment variables with their respective values:
- `VITE_CONTENTFUL_SPACE_ID`
- `VITE_CONTENTFUL_ACCESS_TOKEN`

Then run the following commands:

```bash
npm install
npm run dev
```

The app should be up and running on [http://localhost:5173](http://localhost:5173)
