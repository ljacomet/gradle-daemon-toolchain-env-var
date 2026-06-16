## Basic Gradle project using a specific Daemon Toolchain setup

This project is designed to help investigate potential issues between Gradle and IntelliJ around the sync operation
when daemon toolchain is setup to prevent auto-detection and auto-provisioning.

## Requirements

* An environment variable, `JDK25`, that points at a valid Java 25 JDK installation.
  * That variable must be set in a way that IntelliJ can see it when it starts up. For example, on Linux, that means setting it in `~/.profile` or `~/.bashrc` instead of setting it in a terminal session.

## Validating the setup

* Run `./gradlew help` in a terminal.
* The build should succeed. If not, resolve the `JDK25` env var issue first.

## Exercise the potential issue

* Kill all running Gradle daemons
* Open the project in IntelliJ and trigger a Gradle sync
* Observe the result
  * Sync successfull: The env var was passed by IJ to the TAPI call
  * Sync failed: The env var did not reach the TAPI call, failing the daemon toolchain setup

### My results

* IJ 2025.3.6: the project can sync, which indicates the env var reaches the TAPI
* IJ 2026.1.3: the project cannot sync, which indicates the env var does not reach the TAPI
* IJ 2026.2 EAP: the project can sync, which indicates the env var reaches the TAPI