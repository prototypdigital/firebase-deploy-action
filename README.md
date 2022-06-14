# Firebase deploy

With this action you can deploy Firebase hosting and functions.

## Usage

Create a workflow `.yml` file in your repositories `.github/workflows` directory. Here si an example workflow:

```
name: dev
on:
  push:
    branches:
      - main
jobs:
  build:
    env:
      ENV_SECRETS: ${{ secrets.DEV_SECRETS }}
    runs-on: ubuntu-latest
    steps:
      - uses: prototypdigital/firebase-deploy-action@v1
        with:
          env-secrets: ${{ env.ENV_SECRETS }}
          firebase-token: ${{ secrets.FIREBASE_TOKEN }}
          target: 'dev'
          hosting-message: ${{ github.event.head_commit.message }}
          functions: 'true'
```

## Inputs

Some intputs are required, while others have a default value.

Required:

- `env-secrets` - Your enviroment secrets
- `firebase-token` - Firebase token

Optional:

- `node-version` - Version of node used on project (e.g. '16')
- `fetch-depth` - Number of commits to fetch. 0 indicates all history for all branches and tags. (e.g. '0')
- `target` - Target for hosting if we have multiple Hosting sites (e.g. 'production')
- `hosting-message` - Message for hosting (e.g. ${{ github.event.head_commit.message }})
- `functions` - Do we use Firebase functions, the default value is 'false' ('true' or 'false')
