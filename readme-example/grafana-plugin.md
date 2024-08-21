# Azion Grafana Plugin Data Source Installation

The Azion Grafana plugin data source is ready for local setup. This installation guide assumes you already have Grafana installed and know how to locate the `defaults.ini` file.

If it's installed via Homebrew `defaults.ini` may be in a path similar to this: `/opt/homebrew/Cellar/grafana/11.1.3/share/grafana/conf/defaults.ini`.

It's recommended to install the binary in a folder of preference. When the binary is downloaded, you can choose where to keep it, having more control over the process.

---

## Prerequisites

- Grafana installed (Check this [Grafana installation guide](https://grafana.com/docs/grafana/latest/setup-grafana/installation/) if needed)
- Familiarity with Graffana's installation directory for accessing the `defaults.ini` file

## Installation Steps

1. Open the Grafana folder, and head to `conf` where `defaults.ini` awaits.
2. Open `defaults.ini`, mark `allow_loading_unsigned_plugins = ` and change it to:

   ```
   allow_loading_unsigned_plugins = azion-azion-datasource
   ```

3. Locate the `data` folder within your Grafana installation directory, and create a `plugins` directory inside (create `data` folder if nonexistent).
4. Download the [Azion plugin zip](https://github.com/aziontech/grafana-plugin/releases/latest).
5. Move the zip file to your newly crafted `plugins` directory.
6. Open the terminal, shift to the `plugins` directory and execute:

   ```
   unzip azion-azion-datasource-*.*.*.zip -d ./azion-azion-datasource
   ```

7. Kickstart your Grafana server to accommodate the new plugin.

Typically Grafana uses `localhost:3000`. 

Explore further guides on [using a pre-built dashboard](https://www.azion.com/en/documentation/products/guides/azion-plugin-grafana-pre-built-dash/) and [customizing a dashboard](https://www.azion.com/en/documentation/products/guides/azion-plugin-grafana/) with Azion plugin on Grafana.

---

## Initial Local Setup

For local deployment of the Azion Grafana plugin, follow these steps:

1. Install dependencies:

   ```bash
   yarn
   ```

2. Choose development mode or watch mode:

   ```bash
   yarn dev
   # or
   yarn watch
   ```

3. For production mode, build the plugin:

   ```bash
   yarn build
   ```

4. Test using Jest:

   ```bash
   # Run tests and watch for changes
   yarn test

   # Stop after all tests are run
   yarn lint:ci
   ```

5. Use Docker to run Grafana and the plugin:

   ```bash
   yarn server
   yarn dev 
   ```

6. Run the linter if needed:

   ```bash
   yarn lint   
   # or
   yarn lint:fix
   ```
