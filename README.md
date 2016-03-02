# Gradle QuickStart Demo Application for FXLauncher

This example showcases how to configure [FXLauncher](https://github.com/edvin/fxlauncher) in your
Gradle based application to provide automatic updates optionally in combination with native installers.

Please see [build.gradle](/build.gradle) for more information.

**Note**: There is nothing Gradle spesific about FXLauncher, and these operations should be easy to perform in any build system.
	There is also a [Maven version](https://github.com/edvin/fxldemo) of this project. 

## Operations

The build script supports the following operations:

- **buildApp**: Assembles the application into build/libs
- **deployApp**: Transfers application to appDeployTarget via scp
- **installer**: Generates native installer

### Configuration

Copy the deployment descriptor and customize the following properties:

```groovy
// Installer Filename without suffix
def appFilename = 'FxlDemo'

// The JavaFX Application class name
def appMainClass = 'no.tornado.FxlDemo'

// Optional parameters to the application, will be embedded in the launcher and can be overriden on the command line
def appParameters = '--myOption=myValue --myOtherOption=myOtherValue'

// The Application vendor used by javapackager
def appVendor = 'AcmeInc'

// The Application version used by javapackager
def appVersion = '2.0'

// Base URL where you will host the application artifacts
def appUrl = 'http://fxldemo.tornado.no/'

// Optional scp target for application artifacts hosted at the above url
def appDeployTarget = 'w48839@fxldemo.tornado.no:fxldemo'
```
 
### Prebuilt installers

See http://fxldemo.tornado.no for a prebuilt version of this application, including native installers
for Windows, MacOSX and Linux.