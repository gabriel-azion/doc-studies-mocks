# Vulcan.config.js file

The `vulcan.config.js` file serves as a powerful configuration system for Vulcan, offering customization options for your application's build process. While not mandatory, this file acts as an override mechanism, allowing you to define properties that supersede preset configurations. Unspecified properties will default to preset values.

## Configuration Properties

| Property | Type | Description |
| --- | --- | --- |
| Entry | String | Represents the primary entry point for your application, where the building process begins. Note: Entry will be ignored for Jamstack solutions. |
| Builder | String ('esbuild' or 'webpack') | Defines the build tool to use. Options include esbuild and webpack. |
| UseNodePolyfills | Boolean | Determines whether Node.js polyfills should be applied. Useful for projects leveraging Node.js functionalities targeting environments without built-in capabilities. |
| UseOwnWorker | Boolean | Indicates that the constructed code inserts its own worker expression, eliminating the need to inject a provider. |
| Preset | Object | Provides preset-specific configurations. <br> - Name (Type: String): Refers to the preset name (example: "vue" or "next"). <br>- Mode (Type: String): Specifies the mode for the preset (example: "compute" or "deliver"). |
| MemoryFS | Object | Configurations related to the in-memory filesystem.<br> - InjectionDirs (Type: Array of Strings): Directories injected into memory for runtime access via the fs API. <br>- RemovePathPrefix (Type: String): Prefix path to be removed from files before injecting into memory. |
| Custom | Object | Allows extending the capabilities of the chosen bundler (webpack or esbuild) with custom plugins or configurations.<br>- Plugins (Type: Object): Add custom plugins for the chosen bundler here. |


## Example Configuration

For a Vue-based project:

```javascript
module.exports = {
  entry: 'src/index.js',
  builder: 'webpack',
  useNodePolyfills: true,
  useOwnWorker: false,
  preset: {
    name: 'vue',
    mode: 'compute',
  },
  memoryFS: {
    injectionDirs: ['.faststore/@generated/graphql'],
    removePathPrefix: '.faststore/',
  },
  custom: {
    plugins: {},
  },
};
```
