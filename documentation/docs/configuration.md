---
# !!! DO NOT MODIFY !!!
# This file is auto-generated by the gendoc tool based on the source code of the app.
description: This section describes the configuration parameters and their types for INX-api-core-v1.
keywords:
- IOTA Node 
- Hornet Node
- Configuration
- JSON
- Customize
- Config
- reference
---


# Core Configuration

INX-api-core-v1 uses a JSON standard format as a config file. If you are unsure about JSON syntax, you can find more information in the [official JSON specs](https://www.json.org).

You can change the path of the config file by using the `-c` or `--config` argument while executing `inx-api-core-v1` executable.

For example:
```bash
inx-api-core-v1 -c config_defaults.json
```

You can always get the most up-to-date description of the config parameters by running:

```bash
inx-api-core-v1 -h --full
```

## <a id="app"></a> 1. Application

| Name                      | Description                                            | Type    | Default value |
| ------------------------- | ------------------------------------------------------ | ------- | ------------- |
| checkForUpdates           | Whether to check for updates of the application or not | boolean | true          |
| [shutdown](#app_shutdown) | Configuration for shutdown                             | object  |               |

### <a id="app_shutdown"></a> Shutdown

| Name                     | Description                                                                                            | Type   | Default value |
| ------------------------ | ------------------------------------------------------------------------------------------------------ | ------ | ------------- |
| stopGracePeriod          | The maximum time to wait for background processes to finish during shutdown before terminating the app | string | "5m"          |
| [log](#app_shutdown_log) | Configuration for Shutdown Log                                                                         | object |               |

### <a id="app_shutdown_log"></a> Shutdown Log

| Name     | Description                                         | Type    | Default value  |
| -------- | --------------------------------------------------- | ------- | -------------- |
| enabled  | Whether to store self-shutdown events to a log file | boolean | true           |
| filePath | The file path to the self-shutdown log              | string  | "shutdown.log" |

Example:

```json
  {
    "app": {
      "checkForUpdates": true,
      "shutdown": {
        "stopGracePeriod": "5m",
        "log": {
          "enabled": true,
          "filePath": "shutdown.log"
        }
      }
    }
  }
```

## <a id="logger"></a> 2. Logger

| Name                                     | Description                                                                 | Type    | Default value |
| ---------------------------------------- | --------------------------------------------------------------------------- | ------- | ------------- |
| level                                    | The minimum enabled logging level                                           | string  | "info"        |
| disableCaller                            | Stops annotating logs with the calling function's file name and line number | boolean | true          |
| disableStacktrace                        | Disables automatic stacktrace capturing                                     | boolean | false         |
| stacktraceLevel                          | The level stacktraces are captured and above                                | string  | "panic"       |
| encoding                                 | The logger's encoding (options: "json", "console")                          | string  | "console"     |
| [encodingConfig](#logger_encodingconfig) | Configuration for encodingConfig                                            | object  |               |
| outputPaths                              | A list of URLs, file paths or stdout/stderr to write logging output to      | array   | stdout        |
| disableEvents                            | Prevents log messages from being raced as events                            | boolean | true          |

### <a id="logger_encodingconfig"></a> EncodingConfig

| Name        | Description                                                                                                | Type   | Default value |
| ----------- | ---------------------------------------------------------------------------------------------------------- | ------ | ------------- |
| timeEncoder | Sets the logger's timestamp encoding. (options: "nanos", "millis", "iso8601", "rfc3339" and "rfc3339nano") | string | "rfc3339"     |

Example:

```json
  {
    "logger": {
      "level": "info",
      "disableCaller": true,
      "disableStacktrace": false,
      "stacktraceLevel": "panic",
      "encoding": "console",
      "encodingConfig": {
        "timeEncoder": "rfc3339"
      },
      "outputPaths": [
        "stdout"
      ],
      "disableEvents": true
    }
  }
```

## <a id="db"></a> 3. Database

| Name                 | Description                                                                      | Type    | Default value |
| -------------------- | -------------------------------------------------------------------------------- | ------- | ------------- |
| [tangle](#db_tangle) | Configuration for tangle                                                         | object  |               |
| [utxo](#db_utxo)     | Configuration for UTXO                                                           | object  |               |
| debug                | Ignore the check for corrupted databases (should only be used for debug reasons) | boolean | false         |

### <a id="db_tangle"></a> Tangle

| Name | Description                            | Type   | Default value     |
| ---- | -------------------------------------- | ------ | ----------------- |
| path | The path to the tangle database folder | string | "database/tangle" |

### <a id="db_utxo"></a> UTXO

| Name | Description                          | Type   | Default value   |
| ---- | ------------------------------------ | ------ | --------------- |
| path | The path to the UTXO database folder | string | "database/utxo" |

Example:

```json
  {
    "db": {
      "tangle": {
        "path": "database/tangle"
      },
      "utxo": {
        "path": "database/utxo"
      },
      "debug": false
    }
  }
```

## <a id="protocol"></a> 4. Protocol

| Name      | Description                                       | Type   | Default value       |
| --------- | ------------------------------------------------- | ------ | ------------------- |
| networkID | The network ID on which this app operates on      | string | "chrysalis-mainnet" |
| bech32HRP | The HRP which should be used for Bech32 addresses | string | "iota"              |

Example:

```json
  {
    "protocol": {
      "networkID": "chrysalis-mainnet",
      "bech32HRP": "iota"
    }
  }
```

## <a id="restapi"></a> 5. RestAPI

| Name                      | Description                                                                                   | Type    | Default value    |
| ------------------------- | --------------------------------------------------------------------------------------------- | ------- | ---------------- |
| bindAddress               | The bind address on which the chrysalis API HTTP server listens                               | string  | "localhost:9094" |
| advertiseAddress          | The address of the chrysalis API HTTP server which is advertised to the INX Server (optional) | string  | ""               |
| [limits](#restapi_limits) | Configuration for limits                                                                      | object  |                  |
| swaggerEnabled            | Whether to provide swagger API documentation under endpoint "/swagger"                        | boolean | false            |
| debugRequestLoggerEnabled | Whether the debug logging for requests should be enabled                                      | boolean | false            |

### <a id="restapi_limits"></a> Limits

| Name          | Description                                                               | Type   | Default value |
| ------------- | ------------------------------------------------------------------------- | ------ | ------------- |
| maxBodyLength | The maximum number of characters that the body of an API call may contain | string | "1M"          |
| maxResults    | The maximum number of results that may be returned by an endpoint         | int    | 1000          |

Example:

```json
  {
    "restAPI": {
      "bindAddress": "localhost:9094",
      "advertiseAddress": "",
      "limits": {
        "maxBodyLength": "1M",
        "maxResults": 1000
      },
      "swaggerEnabled": false,
      "debugRequestLoggerEnabled": false
    }
  }
```

## <a id="inx"></a> 6. INX

| Name                  | Description                                                                                        | Type    | Default value    |
| --------------------- | -------------------------------------------------------------------------------------------------- | ------- | ---------------- |
| enabled               | Whether to connect to a node via INX                                                               | boolean | false            |
| address               | The INX address to which to connect to                                                             | string  | "localhost:9029" |
| maxConnectionAttempts | The amount of times the connection to INX will be attempted before it fails (1 attempt per second) | uint    | 30               |
| targetNetworkName     | The network name on which the node should operate on (optional)                                    | string  | ""               |

Example:

```json
  {
    "inx": {
      "enabled": false,
      "address": "localhost:9029",
      "maxConnectionAttempts": 30,
      "targetNetworkName": ""
    }
  }
```

## <a id="profiling"></a> 7. Profiling

| Name        | Description                                       | Type    | Default value    |
| ----------- | ------------------------------------------------- | ------- | ---------------- |
| enabled     | Whether the profiling component is enabled        | boolean | false            |
| bindAddress | The bind address on which the profiler listens on | string  | "localhost:6060" |

Example:

```json
  {
    "profiling": {
      "enabled": false,
      "bindAddress": "localhost:6060"
    }
  }
```

## <a id="prometheus"></a> 8. Prometheus

| Name            | Description                                                     | Type    | Default value    |
| --------------- | --------------------------------------------------------------- | ------- | ---------------- |
| enabled         | Whether the prometheus plugin is enabled                        | boolean | false            |
| bindAddress     | The bind address on which the Prometheus HTTP server listens on | string  | "localhost:9312" |
| goMetrics       | Whether to include go metrics                                   | boolean | false            |
| processMetrics  | Whether to include process metrics                              | boolean | false            |
| restAPIMetrics  | Whether to include restAPI metrics                              | boolean | true             |
| inxMetrics      | Whether to include INX metrics                                  | boolean | true             |
| promhttpMetrics | Whether to include promhttp metrics                             | boolean | false            |

Example:

```json
  {
    "prometheus": {
      "enabled": false,
      "bindAddress": "localhost:9312",
      "goMetrics": false,
      "processMetrics": false,
      "restAPIMetrics": true,
      "inxMetrics": true,
      "promhttpMetrics": false
    }
  }
```

