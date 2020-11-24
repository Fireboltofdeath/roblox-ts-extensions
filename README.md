# Roblox-TS Extensions
This is a Language Service plugin that changes autocompletes based on their network boundary (server / shared)
Currently this only has the aforementioned functionality, however, I do plan to add more in the future so feel free to file an issue.

## Installation
You install this like you would any npm package.

`npm install --save-dev roblox-ts-extensions`

To enable the plugin and configure it, please look to the sections below.

## Configuration
```ts
interface PluginConfig {
	// The directories to be determined client-sided. Rojo is preferred, however these can override Rojo if necessary.
	// Default: []
	client: string | string[];

	// The directories to be determined server-sided. Rojo is preferred, however these can override Rojo if necessary.
	// Default: []
	server: string | string[];

	// The autocomplete mode to use.
	// Prefix: Prefixes completes with their network boundary, and makes cross-boundary (client<->server, shared->client/server) imports type only.
	// Remove: Removes any cross-boundary imports entirely. Does not affect manual imports or existing imports.
	// Default: prefix
	mode: "prefix" | "remove";

	// Whether to use Rojo to calculate server/client boundaries. The client and server properties can override certain directories if necessary.
	// Default: true
	useRojo: boolean;

	// Only works on prefix mode
	// When importing a new cross-boundary import, fix existing import.
	// Example: import { MyClientClass } -> import type { MyClientClass, MyOtherClientClass }
	convertExistingImports: boolean;
}
```


## Enabling
To enable the plugin, add the following "plugins" field to your tsconfig's compilerOptions. You can configure the plugin however you'd like, as shown above.
```jsonc
{
	"compilerOptions": {
		// ...
		"plugins": [
			{
				"name": "roblox-ts-extensions",

				// All the following fields are optional and will use their defaults if omitted.

				"client": [],
				"server": [],
				"mode": "prefix",
				"useRojo": true
			}
		]
	}
}
```
