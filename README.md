name: CI Pipeline to staging/production environment
on:
  pull_request:
    branches:
      - staging
      - main
jobs:
  test:
    runs-on: ubuntu-latest
    name: Setup, test, and build project
    env:
      PORT: 5001
    steps:
      - name: Checkout
        uses: actions/checkout@v3

      - name: Install dependencies
        run: npm ci

      - name: Test application
        run: npm test

      - name: Build application
        run: |
          echo "Run command to build the application if present"
          npm run build --if-present
