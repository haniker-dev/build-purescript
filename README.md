# Github Action build-purescript

## TODO
- Better build script: Currently we use an opinionated way that works for Halogen and Parcel
- Add tag v1 and publish to Github marketplace

## Usage

In your own workflow, add the following action:
```
      - name: Build Purescript App
        uses: haniker-dev/build-purescript@main
        with:
          node-version: "16.x"
          build-dir: "dist"
          entry-html: "public/index.html"
```

## Full Example:

```
name: Build and Deploy
"on":
  push:
    branches:
      - main
jobs:
  deploy-production:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout branch
        uses: actions/checkout@v2

      - name: Build Purescript App
        uses: haniker-dev/build-purescript@main
        with:
          node-version: "16.x"
          build-dir: "dist"
          entry-html: "public/index.html"

      - name: Deploy to Firebase Hosting
        uses: FirebaseExtended/action-hosting-deploy@v0
        with:
          repoToken: "${{ secrets.GITHUB_TOKEN }}"
          firebaseServiceAccount: "${{ secrets.FIREBASE_SERVICE_ACCOUNT_HANIKER_WEBSITE }}"
          channelId: live
          projectId: haniker-website
```
