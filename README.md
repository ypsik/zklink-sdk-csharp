# zklink-sdk-csharp

C# bindings for the [zkLink Rust SDK](https://github.com/zkLinkProtocol/zklink_sdk), generated via [uniffi-bindgen-cs](https://github.com/NordSecurity/uniffi-bindgen-cs).

This provides C# implementation of zkLink order/contract signing — used by zkLink-based exchanges such as [APEX Omni](https://omni.apex.exchange).

## NuGet Package

```
dotnet add package ZkLink.Cs.Sdk
```

Includes prebuilt native libraries for both Windows (x64) and Linux (x64) — no manual DLL handling required.

## Usage

```csharp
using uniffi.zklink_sdk;

var signer = ZkLinkSigner.NewFromSeed(seedBytes);
var publicKey = signer.PublicKey();
```

## Verified

This implementation has been verified end-to-end against APEX Omni's live testnet:
- Derived `l2Key` from an Omni Key seed in C#, confirmed it matches the `l2Key` APEX's own servers report for the account
- Built and signed a full `Contract` order entirely in C#
- Submitted via the real `/v3/order` endpoint — accepted and confirmed live

## Build Pipeline

The `.github/workflows/build-zklink-bindings.yml` workflow:
1. Compiles the `zklink_sdk` Rust crate natively for both Linux and Windows
2. Generates C# bindings via `uniffi-bindgen-cs`
3. Packages everything into a ready-to-use NuGet package

Fully reproducible — no manual steps beyond triggering the workflow.

## License

This repository wraps [zkLinkProtocol/zklink_sdk](https://github.com/zkLinkProtocol/zklink_sdk) (Apache 2.0). See the submodule for the original license.
