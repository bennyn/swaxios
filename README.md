![Swaxios](https://github.com/bennyn/swaxios/raw/master/logo.png)

# Swaxios

A [Swagger](https://swagger.io/) API client generator based on [axios](https://github.com/axios/axios) and written in [TypeScript](https://www.typescriptlang.org/).

## Installation

You can install Swaxios globally (`npm i -g swaxios`) or name it in your [devDependencies](https://docs.npmjs.com/files/package.json#devdependencies).

## Usage

Display all CLI options:

```
swaxios --help
```

If you pass an [OpenAPI Specification (OAS)](https://swagger.io/docs/specification/2-0/basic-structure/) (v2.0; JSON or YAML) to Swaxios, then it generates an API client that uses axios under the hood and is written in TypeScript:

```
# Provide a Swagger input file (JSON or YAML)
swaxios -i ./path/to/swagger.json -o ./path/to/output/directory
swaxios -i ./path/to/swagger.yml -o ./path/to/output/directory

# Alternative: Provide a URL to a Swagger endpoint
swaxios -i http://127.0.0.1:3000/documentation-json -o ./path/to/output/directory
```

With the `-f` option, you can force Swaxios to overwrite existing files in the output path:

```
swaxios -i ./path/to/swagger.json -o ./path/to/output/directory -f
```

## Examples

You can find many examples of generated API client code in our [snapshots section](./src/test/snapshots).

Here is a simple example:

**`ExchangeService.ts`**

```ts
/* tslint:disable */

/**
 * This file was automatically generated by "Swaxios".
 * It should not be modified by hand.
 */

import {AxiosInstance} from 'axios';

export class ExchangeService {
  private readonly apiClient: AxiosInstance;

  constructor(apiClient: AxiosInstance) {
    this.apiClient = apiClient;
  }

  deleteExchange = async (id: number): Promise<void> => {
    const resource = `/api/v1/exchange/${id}`;
    await this.apiClient.delete(resource);
  };
}
```

It has been generated from the following [path](https://swagger.io/docs/specification/2-0/paths-and-operations/):

**`swagger.json`**

```jsonc
{
  ...,
  "paths": {
    "/api/v1/exchange/{id}": {
      "delete": {
        "consumes": [
          "application/json"
        ],
        "operationId": "deleteExchange",
        "parameters": [
          {
            "in": "path",
            "name": "id",
            "required": true,
            "type": "number"
          }
        ],
        "produces": [
          "application/json"
        ],
        "responses": {
          "200": {
            "description": ""
          }
        }
      }
    }
  },
  ...
}
```

## Credits

This project is inspired by [swagger-codegen](https://github.com/swagger-api/swagger-codegen).
