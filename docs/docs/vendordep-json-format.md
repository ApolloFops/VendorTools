---
layout: default
title: Vendordep JSON Format
nav_order: 1
---

# Vendordep JSON Format
{: .no_toc }

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

{: .highlight }
These docs are incomplete! Feel free to help expand them if you know more about how this format
works, I'm not an expert and I haven't asked anyone who is yet (most of this is just inferred or
deduced from the source code).

## Sample

```json
{
	"fileName": "MyLibrary-2026.0.0.json",
	"name": "MyLibrary",
	"version": "2026.0.0",
	"frcYear": "2026",
	"uuid": "<UUID>",
	"mavenUrls": [
		"https://maven.example.com/mylibrary/"
	],
	"jsonUrl": "https://example.com/MyLibrary/mylibrary.json",
	"conflictsWith": [
        {
            "uuid": "e7900d8d-826f-4dca-a1ff-182f658e98af",
            "errorMessage": "Users can not have both the MyLibrary and the MyLibrary-orange dependencies in their project.",
            "offlineFileName": "MyLibrary-orange.json"
        }
    ],
	"requires": [
		{
			"uuid": "3f48eb8c-50fe-43a6-9cb7-44c86353c4cb",
			"errorMessage": "OtherLib is required!",
			"offlineFileName": "OtherLib.json",
			"onlineUrl": "https://example.com/OtherLib.json"
		},
	],
	"javaDependencies": [
		{
			"groupId": "com.example.mylibrary",
			"artifactId": "MyLibrary-java",
			"version": "2026.0.0"
		}
	],
	"jniDependencies": [
		{
            "groupId": "com.example.mylibrary",
            "artifactId": "MyLibrary-driver",
            "version": "2026.0.0",
            "isJar": false,
            "skipInvalidPlatforms": true,
            "validPlatforms": [
                "windowsx86-64",
                "linuxarm64",
                "linuxx86-64",
                "linuxathena",
                "linuxarm32",
                "osxuniversal"
            ]
        }
	],
	"cppDependencies": [
		{
            "groupId": "com.example.mylibrary",
            "artifactId": "MyLibrary-cpp",
            "version": "2026.0.0",
            "libName": "MyLibrary",
            "headerClassifier": "headers",
            "sharedLibrary": false,
            "skipInvalidPlatforms": true,
            "binaryPlatforms": [
                "windowsx86-64",
                "linuxarm64",
                "linuxx86-64",
                "linuxathena",
                "linuxarm32",
                "osxuniversal"
            ]
        },
        {
            "groupId": "com.example.mylibrary",
            "artifactId": "MyLibrary-driver",
            "version": "2026.0.0",
            "libName": "MyLibraryDriver",
            "headerClassifier": "headers",
            "sharedLibrary": false,
            "skipInvalidPlatforms": true,
            "binaryPlatforms": [
                "windowsx86-64",
                "linuxarm64",
                "linuxx86-64",
                "linuxathena",
                "linuxarm32",
                "osxuniversal"
            ]
        }
	]
}
```

## Fields

### fileName

The filename to save the vendordep as when the user downloads it. This can be different from the
filename on the webserver.

### name

The name of the vendordep.

### version

The version of the vendordep.

### frcYear

The year number this vendordep is compatible with.

### uuid

A UUID for this vendordep. You can generate one of these with [this
generator](https://guidgenerator.com/online-guid-generator.aspx).

### mavenUrls

A list of Maven repository URLs for this library. These store both the Java and the C++ dependencies.

### jsonUrl

The URL to the latest version of this vendor JSON.

### conflictsWith

A list of other vendor dependencies that this dependency conflicts with, with the following schema.

| Name              | Description                                                     | Sample                                                                                          |
| :---------------- | :-------------------------------------------------------------- | :---------------------------------------------------------------------------------------------- |
| `uuid`            | The unique identifier for this vendor dependency.               | `e7900d8d-826f-4dca-a1ff-182f658e98af`                                                          |
| `errorMessage`    | An error message to display when the other dependency is found. | `Users can not have both the MyLibrary and the MyLibrary-orange dependencies in their project.` |
| `offlineFileName` | The file name of the other dependency.                          | `MyLibrary-orange.json`                                                                         |

### requires

A list of other vendor dependencies that this dependency requires, with the following schema.

| Name              | Description                                                         | Sample                                 |
| :---------------- | :------------------------------------------------------------------ | :------------------------------------- |
| `uuid`            | The unique identifier for this vendor dependency.                   | `3f48eb8c-50fe-43a6-9cb7-44c86353c4cb` |
| `errorMessage`    | An error message to display when the other dependency is not found. | `OtherLib is required!`                |
| `offlineFileName` | The file name that the other dependency can be found as.            | `OtherLib.json`                        |
| `onlineUrl`       | The URL where the dependency JSON can be found.                     | `https://example.com/OtherLib.json`    |


### javaDependencies

A list of Java Maven dependencies with the following schema.

| Name         | Description                               | Sample                  |
| :----------- | :---------------------------------------- | :---------------------- |
| `groupId`    | The Maven Group ID for the dependency.    | `com.example.mylibrary` |
| `artifactId` | The Maven Artifact ID for the dependency. | `MyLibrary-java`        |
| `version`    | The Maven Version for the dependency.     | `2026.0.0`              |

### jniDependencies

A list of Java Native Interface C dependencies with the following schema.

| Name                   | Description                                                                                                                | Sample                                                                                          |
| :--------------------- | :------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------- |
| `groupId`              | The Maven Group ID for the dependency.                                                                                     | `com.example.mylibrary`                                                                         |
| `artifactId`           | The Maven Artifact ID for the dependency.                                                                                  | `MyLibrary-driver`                                                                              |
| `version`              | The Maven Version for the dependency.                                                                                      | `2026.0.0`                                                                                      |
| `isJar`                | Is this archive in the form of a jarfile? I haven't seen this used before, so I can't make any guarantees on how it works. | `false`                                                                                         |
| `skipInvalidPlatforms` | Should we skip any invalid platforms in the list?                                                                          | `true`                                                                                          |
| `validPlatforms`       | A list of platforms this dependency supports.                                                                              | `[ "windowsx86-64", "linuxarm64", "linuxx86-64", "linuxathena", "linuxarm32", "osxuniversal" ]` |

### cppDependencies

A list of C++ dependencies with the following schema.

| Name                   | Description                                       | Sample                                                                                          |
| :--------------------- | :------------------------------------------------ | :---------------------------------------------------------------------------------------------- |
| `groupId`              | The Maven Group ID for the dependency.            | `com.example.mylibrary`                                                                         |
| `artifactId`           | The Maven Artifact ID for the dependency.         | `MyLibrary-cpp`                                                                                 |
| `version`              | The Maven Version for the dependency.             | `2026.0.0`                                                                                      |
| `libName`              | The name of the C++ library.                      | `MyLibrary`                                                                                     |
| `headerClassifier`     |                                                   | `headers`                                                                                       |
| `sharedLibrary`        |                                                   | `true`                                                                                          |
| `skipInvalidPlatforms` | Should we skip any invalid platforms in the list? | `true`                                                                                          |
| `validPlatforms`       | A list of platforms this dependency supports.     | `[ "windowsx86-64", "linuxarm64", "linuxx86-64", "linuxathena", "linuxarm32", "osxuniversal" ]` |
