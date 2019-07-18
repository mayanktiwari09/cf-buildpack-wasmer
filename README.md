# cf-buildpack-wasmer

This is a Cloud Foundry buildpack for [Wasmer](https://wasmer.io/).

## Example

The full example of running Nginx with Wasmer is available [here](https://github.com/jingweno/nginx-wasmer).

Set up project to use with [wapm](https://wapm.io/):

```
wapm init nginx-wasmer
```

Add a "dependencies" section to wapm.toml according to https://wapm.io/help/reference. For example:

```
$ cat wapm.toml
[package]
name = "nginx-wasm"
version = "0.1.0"
description = ""

[dependencies]
nginx = "0.1.1"
```

Add a `Procfile` that runs Nginx with Wasmer. The following script substitute Nginx port with the environment variable `$PORT`:

```
$ cat Procfile
web: wasmer run nginx.wasm -- -p . -c nginx.conf
```
Check [Example-Repository](https://github.com/mayanktiwari09/cf-ngnix-wasmer)  
Create a Cloud Foundry app, set the buildpack and deploy:

```
cf push wasm-ngnix -b https://github.com/mayanktiwari09/cf-buildpack-wasmer.git
```
