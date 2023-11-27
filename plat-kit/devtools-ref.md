# Azion Platform Kit

<---Button que leva para o repo --->

Azion Platform Kit is a front-end development kit designed for running a customized Azion Real-time Manager. This kit is built using Vue/Vite and incorporates the PrimeVue and Tailwind frameworks.

## Getting Started

### Requirements

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
   curl https://downloads.azion.com/linux/x86_64/azion -o azion && chmod +x azion
   ./azion -t PERSONALTOKEN
   ```

3. Link project to an edge application:

   ```bash
   azion link
   ```

   After a few seconds, access your project on the domain provided by the CLI.

## Features - outro termo talvez fique melhor

The Azion Platform Kit includes the following features:

- Multi-tenancy: build your Real-Time Manager by consuming endpoints from the [Azion Public API](https://api.azion.com/).
- Customizable UI: configure theme tokens or generate them automatically via the Builder, giving the look and feel according to your needs.
- Simple Structure: layered separation of blocks, components, and services for easy route building.

## Contributing

Before contributing to the project, please familiarize yourself with: 
- The [Contributor Guide](CONTRIBUTING.md)
- [Development Guide](DEVELOPER.md) to set up your development environment.
- [UX Write guidelines]()


