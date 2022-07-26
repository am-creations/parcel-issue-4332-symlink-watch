# parcel-issue-4332-symlink-watch
Minimal repro repository for https://github.com/parcel-bundler/parcel/issues/4332

# How to reproduce

NPM install both root and local NPM library

```shell
cd src 
npm install

cd ../vendor/myLib
npm install
```

Run watch on both root and local NPM library on separate shells

```shell
cd src 
npm run watch
```

```shell
cd ../vendor/myLib
npm run my.lib.watch
```

* Apply changes to the code inside the library (src/index.ts)
* Observe the lack of change notification in the first watch, even when stopping+restart the watc

# Notes

The issue is the same when using "local" NPM dependencies like this :

```json5
{
  "dependencies": {
    "@my/lib": "file:../vendor/myLib"
  }
}
```