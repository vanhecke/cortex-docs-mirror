---
description: >-
  Troubleshoot Docker installation, container, and runtime issues on Cortex
  XSIAM engines.
---

# Troubleshoot Docker Issues

The following provides troubleshooting solutions for Docker networking and performance issues.

**Troubleshoot Docker networking issues**

In Cortex XSIAM, integrations and scripts run either on the tenant, or on an engine.

If you have Docker networking issues when using an engine, you need to modify the d1.conf file.

1. On the machine where the Engine is installed, open the **`d1.conf`** file.
2.  Add the following to the **`d1.conf`** file:

    ```
    {
    	"LogLevel": "info",
    	"LogFile": "/var/log/demisto/d1.log",
    	"EngineURLs": [
    	"wss://1234.demisto.live/d1ws"
    	],
    					"BindAddress": ":443",
    	"EngineID": "XYZ",
    	"ServerPublic": "ABC"
    	"ArtifactsFolder": "",
    	"TempFolder": "",
    	"python.pass.extra.keys": "--network=host"
    	}
    ```
3. Save the file.
4. Restart the engine using **`systemctl restart d1`** or **`service d1 restart`**.

Troubleshoot Docker performance issues

This information is intended to help resolve the following Docker performance issues.

* Containers are getting stuck.
* The Docker process consumes a lot of resources.
* Time synchronization issues between the container and the operating system.

**Cause**

The installed Docker package and its dependencies are not up to date.

**Workaround**

1.  Update the package manager cache.

    | Linux Distribution | Command              |
    | ------------------ | -------------------- |
    | Debian             | **`apt-get update`** |
2.  (Optional) Check for a newer version of the Docker package.

    | Linux Distribution | Command                       |
    | ------------------ | ----------------------------- |
    | Debian             | **`apt-cache policy docker`** |
3.  Update the Docker package.

    | Linux Distribution | Command                     |
    | ------------------ | --------------------------- |
    | Debian             | **`apt-get update docker`** |
