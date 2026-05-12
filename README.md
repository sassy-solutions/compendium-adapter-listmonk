# `compendium-adapter-listmonk`

[Listmonk](https://listmonk.app/) email service adapter for the [Compendium](https://github.com/sassy-solutions/compendium) event-sourcing framework. Implements `IEmailService` from `Compendium.Abstractions.Email` for transactional emails, newsletter management, and subscriber management via Listmonk's REST API.

Extracted from `sassy-solutions/compendium` per [ADR-0006](https://github.com/sassy-solutions/compendium/blob/main/docs/adr/0006-multi-repo-adapter-split.md) (multi-repo adapter split). Built from [`template-compendium-adapter-dotnet`](https://github.com/sassy-solutions/template-compendium-adapter-dotnet).

## Install

```bash
dotnet add package Compendium.Adapters.Listmonk
```

```csharp
services.AddListmonkEmail(builder.Configuration.GetSection("Listmonk"));
```

See [`docs/README.md`](docs/README.md) for full configuration, subscriber management, and webhook handling.

## Versioning

This package continues the version sequence of `Compendium.Adapters.Listmonk` originally published from the framework monorepo (last framework-published version: `1.0.0-preview.8`). The first release from this repo is `v1.0.0-preview.9`. Versions are driven by git tags via [MinVer](https://github.com/adamralph/minver) — see [`docs/RELEASE.md`](docs/RELEASE.md).

## Repository conventions

| Aspect | Choice |
|---|---|
| Target | .NET 9, C# 13 |
| Test framework | xUnit 2.9.3 + FluentAssertions 6.12.1 + NSubstitute 5.1.0 |
| Coverage | currently **98.64 %** line / 88.33 % branch (124 tests) — gate at 90 % line |
| HTTP mocking | `RichardSzalay.MockHttp` 7.0.0 |
| Result pattern | `Result<T>` from `Compendium.Core` |
| Test naming | `{SUT}Tests` / `{Method}_{Scenario}_{Expected}` + AAA explicit |

## Known cleanup TODO

- `CS1998` is suppressed in `Directory.Build.props` because `ListmonkEmailService` has async methods without await. Inherited from the framework's pre-extraction source. Refactor to `Task.FromResult` / sync signatures and remove the suppression in a future PR.

## Build & test locally

```bash
dotnet restore
dotnet build -c Release
dotnet test -c Release --collect:"XPlat Code Coverage"
```

## License

[MIT](LICENSE) — Copyright © 2026 Sassy Solutions.
