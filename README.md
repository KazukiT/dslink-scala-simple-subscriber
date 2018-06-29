# dslink-scala-simple-subscriber
Subscribe a DSA node then print it on update

# Usage

```shell-session
$ sbt assembly
$ java -jar target/scala-2.12/SimpleSubscriberDSLink-assembly-0.1.0-SNAPSHOT.jar <path of node to subscribe>  --broker https://broker-host:port/conn
```

## Example Usage

```shell-session
$ java -jar target/scala-2.12/SimpleSubscriberDSLink-assembly-0.1.0-SNAPSHOT.jar /downstream/System/CPU_Usage --broker https://localhost:8443/conn
```

## Permission note

Starting with Cisco Kinetic Edge and Fog Processing Module 1.2.1, permission feature is enable by default for new
installation.  With such default permission setting, broker permits nothing to DSLink connected from external host.
This is inconvenient when you run broker in a Docker container and you run your DSLink under development on host OS or
another Docker container.  To make broker permissive for external DSLink, you have to change server.json.

There is two simple way to permit everything for external DSLink.  One is making "defaultPermission" empty.

```json
"defaultPermission": null
```

The other way is changing value of "default" entry "config" from "none".

```json
"defaultPermission": [
  [":config","config"],
  [":write","write"],
  [":read","read"],
  [":user","read"],
  [":trustedLink","config"],
  ["default","config"]
```

Note that the above is not recommended permission for production.