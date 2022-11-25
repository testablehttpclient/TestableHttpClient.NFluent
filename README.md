# TestableHttpClient.NFluent

![GitHub](https://img.shields.io/github/license/testablehttpclient/TestableHttpClient.NFluent) ![GitHub Workflow Status](https://img.shields.io/github/workflow/status/testablehttpclient/TestableHttpClient.NFluent/CI) ![Project status](https://img.shields.io/badge/Status-Archived-yellow) ![Nuget](https://img.shields.io/nuget/v/TestableHttpClient.NFluent)

In integration tests, asserting HttpResponseMessages can be a real challenge, especially since error messages are sometimes not very clear. NFluent is known for giving clear error messages.
`TestableHttpClient.NFluent` is designed to make it easier to check `HttpResponseMessage`s and `TestableHttpClient`s and give clear error messages.

For example when the following check fails:
```csharp
Check.That(response).HasResponseHeader("Server");
```
it will return the following message:
```
The checked response's headers does not contain the expected header.
The checked response's headers:
    {"Connection"} (1 item)
The expected header:
    ["Server"]
```

## Status

The TestableHttpClient.NFluent has been deprecated and is no longer being maintained.
The main reason for this is that I no longer use NFluent.
If someone wants to continue developing this library, please feel free to contact me.

## How to install

TestableHttpClient.NFluent is released as a NuGet packages and can be installed via the NuGet manager in VisualStudio or by running the following command on the command line:
```
dotnet add package TestableHttpClient.NFluent
```

## How to use

### Asserting HttpResponseMessages

```csharp
var client = new HttpClient();

var result = await httpClient.GetAsync("https://httpbin.org/status/200");

Check.That(result).HasStatusCode(HttpStatusCode.OK).And.HasContentHeader("Content-Type", "*/json*");
```

### Asserting TestableHttpMessageHandler

```csharp
var handler = new TestableHttpMessageHandler();
var client = new HttpClient(handler);

_ = await httpClient.GetAsync("https://httpbin.org/status/200");

Check.That(handler).HasMadeRequestsTo("https://httpbin.org*").WithHttpMethod(HttpMethod.Get);
```

## Authors

* **David Perfors** - [dnperfors](https://github.com/dnperfors)

See also the list of [contributors](https://github.com/testablehttpclient/TestableHttpClient/contributors) who participated in this project.

## License

This project is released under the MIT license, see [LICENSE.md](https://github.com/testablehttpclient/TestableHttpClient/blob/master/LICENSE.md) for more information.
