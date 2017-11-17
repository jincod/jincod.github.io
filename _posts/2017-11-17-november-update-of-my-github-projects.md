---
title: November update of my github projects
tags: [aspnetcore, heroku, dotnetcore, buildpacks, cqrs, refit]
---

## Dotnetcore Buildpack

[dotnetcore-buildpack](https://github.com/jincod/dotnetcore-buildpack)

- Removed `dotnet restore` step
- Extremely optimized slag size (`DOTNET_SKIP_FIRST_TIME_EXPERIENCE:1`)
- Updated .NET Core SDK 2.0.3
- Added support `PROJECT_FILE` and `PROJECT_NAME` environment variables ([#23](https://github.com/jincod/dotnetcore-buildpack/pull/23))

## ASP.NET Core Demo App

[AspNet5DemoApp](https://github.com/jincod/AspNet5DemoApp)

- Updated npm modules and nuget packages
- Added `react-scripts`
- Added `Dockerfile` and `License`

## Jincod.CQRS

[Jincod.CQRS](https://github.com/jincod/Jincod.CQRS)

- Updated .NET Core to 2.0.0
- Updated [nuget](https://www.nuget.org/packages/Jincod.CQRS) package to 2.0.1

## Build scripts

[build-scripts](https://github.com/jincod/build-scripts)

- Fixed setup script
- Added `Cake.Bakery` to pacakges.config

## Strongly Typed Web API Example

[Jincod.CQRS](https://github.com/jincod/StronglyTypedWebAPI)

- Created project for demonstration creating API Controllers using interfaces of services with [Refit](https://github.com/paulcbetts/refit) attributes.
