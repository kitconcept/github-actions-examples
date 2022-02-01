# Github Actions Examples (by kitconcept)

## Checkout private repository

````
name: Checkout volto blocks
on: [push]
jobs:
  build:
    runs-on: ubuntu-latest
    strategy:
      fail-fast: false
      matrix:
        node-version: [14.x]

    steps:
      - uses: actions/checkout@v2

      # checkout the private repo containing the action to run
      - name: Checkout GitHub Action Repo
        uses: actions/checkout@v2
        with:
          repository: kitconcept/volto-blocks
          token: ${{ secrets.KITCONCEPT_GMBH_READ_TOKEN }} # stored in GitHub secrets
          path: src/addons/kitconcept.volto-blocks
      - run: ls -al src/addons/kitconcept.volto-blocks

      # - run: cat mrs.developer.json
      # - run: yarn install
      # - run: npx -p mrs-developer missdev --config=jsconfig.json --output=addons --fetch-https
      - run: make build-frontend
````


## Publish Unit Test Results

````
      - name: Publish Unit Test Results
        uses: EnricoMi/publish-unit-test-result-action@v1
        if: always()
        with:
          files: api/parts/test/testreports/*.xml
````
