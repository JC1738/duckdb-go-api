# duckdb-go-api

Go bindings for the DuckDB C Extension API, enabling DuckDB extensions to be written in Go.

## About This Fork

This repository is a maintained fork originally derived from [taniabogatsch/goofy-duck](https://github.com/taniabogatsch/goofy-duck), which demonstrated writing DuckDB extensions in Go using the C API.

The upstream goofy-duck project is no longer actively maintained. This fork is maintained specifically for [DuckArrow](https://github.com/JC1738/duckarrow), a DuckDB extension that enables querying Apache Arrow Flight SQL servers.

> **Note:** This is different from [duckdb/duckdb-go-bindings](https://github.com/duckdb/duckdb-go-bindings), which provides *client* bindings for Go applications to use DuckDB. This repository provides *extension* API bindings for writing DuckDB extensions in Go.

## Current Version

- **DuckDB C Extension API:** v1.4.0 (LTS)
- **Header files:** `duckdb.h`, `duckdb_go_extension.h`

## Contents

| File | Description |
|------|-------------|
| `duckdb.h` | DuckDB C API header from official release |
| `duckdb_go_extension.h` | Extension API with function pointer struct and static wrappers |
| `api.go` | Go initialization and API access |
| `functions.go` | Go wrappers for DuckDB C functions |
| `enums.go` | Go constants for DuckDB types and states |
| `types.go` | Go type definitions |
| `pointers.go` | Pointer handling utilities |

## Usage

This package is designed to be used as a Git submodule in DuckDB extension projects:

```bash
git submodule add https://github.com/JC1738/duckdb-go-api.git
```

Then import in your Go extension code:

```go
import "duckdb"

//export my_extension_init
func my_extension_init(info unsafe.Pointer, access unsafe.Pointer) bool {
    api, err := duckdb.Init("v1.4.0", info, access)
    if err != nil {
        return false
    }
    // Register functions, table functions, etc.
    return true
}
```

## Updating DuckDB Version

To update to a new DuckDB C API version:

1. Download `duckdb.h` from the [DuckDB release](https://github.com/duckdb/duckdb/releases)
2. Update version macros in `duckdb_go_extension.h`
3. Update `enums.go` if new types/enums were added
4. Update the version string passed to `duckdb.Init()`

## License

MIT License - see [LICENSE](LICENSE)

## Acknowledgments

- Original work by [@taniabogatsch](https://github.com/taniabogatsch) in [goofy-duck](https://github.com/taniabogatsch/goofy-duck)
- [DuckDB](https://duckdb.org/) team for the excellent C Extension API
