# Gradle QuickStart Demo Application for FXLauncher

This example showcases how to configure [FXLauncher](https://github.com/edvin/fxlauncher) in your
Gradle based application to provide automatic updates optionally in combination with native installers.

Please see [build.gradle](/build.gradle) for more information.

**Note**: Even though FXLauncher has a Gradle plugin, there is nothing Gradle spesific about it, and these operations should be easy to perform in any build system.
	There is also a [Maven version](https://github.com/edvin/fxldemo) of this project.

## Operations

The Gradle plugin supports the following tasks:

- **copyAppDependencies**: Assembles the application into `build/fxlauncher`
- **generateApplicationManifest**: Generates app.xml into `build/fxlauncher`
- **embedApplicationManifest**: Copies app.xml into `fxlauncher.jar`
- **deployApp**: Transfers application to `deployTarget` via scp
- **generateNativeInstaller**: Generates native installer

Normally you would only perform `deployApp` to update your application, as all the previous
tasks are dependencies on this one. To test your app locally in `build/fxlauncher` you
only need to run the `embedApplicationManifest` task.

### Configuration

See [build.gradle](/build.gradle) for configuration options.

### Prebuilt installers

See http://fxldemo.tornado.no for a prebuilt version of this application, including native installers
for Windows, MacOSX and Linux.

### Deploy to Amazon S3

The built in `deployApp` task will only deploy using scp. If you want to deploy to Amazy, you can include this task in your build. Make sure
you run the `embedApplicationManifest` before this task.

```groovy
task deployS3(type: Exec) {
    // You need to have installed AWS command line interface: https://aws.amazon.com/cli/
    commandLine 'aws', 'configure', 'set', 'aws_access_key_id', 'your_access_key_id'
    commandLine 'aws', 'configure', 'set', 'aws_secret_access_key', 'your_secret_access_key'
    commandLine 'aws', 's3', 'cp', 'build/libs', appDeployTarget, '--acl', 'public-read', '--recursive', '--region', 'us-west-1'
}
```