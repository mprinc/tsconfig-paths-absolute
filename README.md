# tsconfig-paths-absolute

Testing for the absolute paths support

# Issues

## Absolute paths

```sh
# Will break on the absolute path that is instead of left the same: `/Users/mprinc/data/development/colabo-zontik/colabo-lab/typescript/tsconfig-paths/tsconfig-paths-absolute/a` 
# expanded to `/Users/mprinc/data/development/colabo-zontik/colabo-lab/typescript/tsconfig-paths/tsconfig-paths-absolute`
# When fixed `return path.join(absoluteBaseUrl, pathToResolve);` 
# into `return pathToResolve[0] === "/" ? pathToResolve : path.join(absoluteBaseUrl, pathToResolve);`
# Will work
ts-node -r tsconfig-paths/register index.ts

# Same scenario
node  -r ts-node/register -r tsconfig-paths/register index.ts

tsc
# Doesn't work as it doesn't look for modules under `dist` (probably should create full packages)
node -r tsconfig-paths/register dist/index.js
```

## `baseUrl` for the extending tsconfig

Makes problem if the extending tsconfig is in different folder than the CWD tsconfig and it also has baseUrl
+ baseUrl of the extending tsconfig will be CWD rather than the folder of the extending tsconfig
