# Azion Platform Kit Documentation

Azion Platform Kit is a front-end development kit designed for running a customized Azion Real-time Manager. This kit is built using Vue/Vite and incorporates the PrimeVue and Tailwind frameworks.

## Getting Started

### Prerequisites

Before you begin, ensure that you have the following:

- [Node.js](https://nodejs.org/) version 18 or later
- [Yarn](https://yarnpkg.com/) package manager

### Setup

1. Clone the repository:

   ```bash
   git clone git@github.com:aziontech/azion-platform-kit.git
   cd azion-platform-kit
   ```

2. Install dependencies and start the project:

   ```bash
   yarn install
   yarn dev --host
   ```

   The web app is now accessible at [http://localhost:5173](http://localhost:5173).

### Using Docker

If you prefer not to run things on your machine, you can use Docker:

```bash
alias yarn="docker run -it --rm -p 5173:5173 -v $HOME:/root -v $PWD:/usr/src/app -w /usr/src/app node:18 yarn"
```

## Configuration

### Personal Token

For faster setup, create a personal token in Azion Realtime Manager and save it in a `.env.development` file:

```bash
echo 'VITE_PERSONAL_TOKEN=PERSONALTOKEN' > .env.development
```

### API Configuration

By default, the Platform Kit uses the STAGE stack to connect with Azion APIs. To point your application to the PRODUCTION stack, add the following command in the `.env.development` file:

```bash
VITE_ENVIRONMENT='PRODUCTION'
```

## Running on the Edge

The Azion Platform Kit can run natively on Azion's edge using Azion CLI (version >= 0.70.0). Follow these steps:

1. Download and configure Azion-CLI with a Personal Token:

   ```bash
   curl https://downloads.azion.com/linux/x86_64/azioncli -o azioncli && chmod +x azioncli
   ./azioncli configure -t PERSONALTOKEN
   ```

2. Build the bundler and copy the content to the edge:

   ```bash
   yarn build
   mkdir -p .edge/statics && cp -r ./dist/* .edge/statics
   ```

3. Publish your edge application:

   ```bash
   azioncli edge_applications init --name azion-platform-kit --type vue --mode deliver
   azioncli edge_applications publish --debug
   ```

   After a few seconds, access your project on the domain provided by the CLI.

## Features

The Azion Platform Kit includes the following features:

- Multi-tenancy: build your Real-Time Manager by consuming endpoints from the [Azion Public API](#).
- Customizable UI: configure theme tokens or generate them automatically via the Builder, giving the look and feel according to your needs.
- Simple Structure: layered separation of blocks, components, and services for easy route building.

## Contributing

Before contributing to the project, please familiarize yourself with the [Contributor Guide](CONTRIBUTING.md) and [Development Guide](DEVELOPER.md) to set up your development environment.

## Code of Conduct

Read and adhere to our [Code of Conduct](#).
