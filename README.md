# Repro for issue 8224

## Versions

firebase-tools: v13.31.1
platform: macOS Sonoma 14.7.3

## Steps to reproduce

1. Install dependencies

   - Run `cd frontend`
   - Run `npm i`
   - Run `cd ../`

2. Run `firebase emulators:start --project demo-project --debug`
   - Error is raised

```
$ firebase emulators:start --project demo-project --debug
(node:64688) [DEP0040] DeprecationWarning: The `punycode` module is deprecated. Please use a userland alternative instead.
(Use `node --trace-deprecation ...` to show where the warning was created)
[2025-02-18T11:27:39.812Z] > command requires scopes: ["email","openid","https://www.googleapis.com/auth/cloudplatformprojects.readonly","https://www.googleapis.com/auth/firebase","https://www.googleapis.com/auth/cloud-platform"]
[2025-02-18T11:27:39.813Z] > authorizing via signed-in user (EMAIL)
i  emulators: Starting emulators: apphosting {"metadata":{"emulator":{"name":"hub"},"message":"Starting emulators: apphosting"}}
i  emulators: Detected demo project ID "demo-project", emulated services will use a demo configuration and attempts to access non-emulated services for this project will fail. {"metadata":{"emulator":{"name":"hub"},"message":"Detected demo project ID \"demo-project\", emulated services will use a demo configuration and attempts to access non-emulated services for this project will fail."}}
[2025-02-18T11:27:40.050Z] [logging] Logging Emulator only supports listening on one address (127.0.0.1). Not listening on ::1
[2025-02-18T11:27:40.050Z] [apphosting] App Hosting Emulator only supports listening on one address (127.0.0.1). Not listening on ::1
[2025-02-18T11:27:40.050Z] assigned listening specs for emulators {"user":{"hub":[{"address":"127.0.0.1","family":"IPv4","port":4400},{"address":"::1","family":"IPv6","port":4400}],"logging":[{"address":"127.0.0.1","family":"IPv4","port":4500}],"apphosting":[{"address":"127.0.0.1","family":"IPv4","port":4200}]},"metadata":{"message":"assigned listening specs for emulators"}}
⚠  emulators: It seems that you are running multiple instances of the emulator suite for project demo-project. This may result in unexpected behavior.
[2025-02-18T11:27:40.053Z] [hub] writing locator at /var/folders/6r/csjmhpv13nbbc2wq1mdclkc400t31x/T/hub-demo-project.json
[2025-02-18T11:27:40.101Z] TypeError: Cannot read properties of undefined (reading 'includes')
    at formatHost (/usr/local/lib/node_modules/firebase-tools/lib/emulator/functionsEmulatorShared.js:284:14)
    at setEnvVarsForEmulators (/usr/local/lib/node_modules/firebase-tools/lib/emulator/env.js:9:63)
    at getEmulatorEnvs (/usr/local/lib/node_modules/firebase-tools/lib/emulator/apphosting/serve.js:54:38)
    at serve (/usr/local/lib/node_modules/firebase-tools/lib/emulator/apphosting/serve.js:34:88)
    at process.processTicksAndRejections (node:internal/process/task_queues:105:5)

Error: An unexpected error has occurred.
```

## Notes

Not reproducible using firebase-tools v13.28.0, v13.29.0, v13.29.1 <br>
Reproducible on v13.29.2
