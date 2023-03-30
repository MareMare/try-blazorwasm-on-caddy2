# try-blazorwasm-on-caddy2

* [caddyserver/caddy: Fast and extensible multi\-platform HTTP/1\-2\-3 web server with automatic HTTPS](https://github.com/caddyserver/caddy)
* [Getting Started — Caddy Documentation](https://caddyserver.com/docs/getting-started)
  * [file\_server \(Caddyfile directive\) — Caddy Documentation](https://caddyserver.com/docs/caddyfile/directives/file_server#syntax)
  * [try\_files \(Caddyfile directive\) — Caddy Documentation](https://caddyserver.com/docs/caddyfile/directives/try_files#syntax)

## Blazor WASM (Brotli) の発行
```ps1
dotnet publish .\src\try-blazorwasm-on-caddy2\try-blazorwasm-on-caddy2.csproj -o .output
```

## `Caddyfile`
```Caddyfile
localhost:2019

root * .\.output\wwwroot
try_files {path} /index.html
file_server {
	precompressed br
}

```
**👆 最後の空行がいるみたい。**

## `Caddyfile` の構成を適用して `caddy` を実行
* 方法１
    ```ps1
    caddy adapt --config .\Caddyfile
    caddy run
    ```
* 方法２
    ```ps1
    caddy run --config .\Caddyfile
    ```

