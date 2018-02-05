# Azure Storage Emulator Docker Image
<https://docs.microsoft.com/en-us/azure/storage/storage-use-emulator>

![Docker Build](https://farmer1992.visualstudio.com/_apis/public/build/definitions/3686302e-40e0-495b-a6f8-f2926767661b/9/badge)

## Usage 

```
docker run -p 10000:10000 -p 10001:10001 -p 10002:10002 farmer1992/azure-storage-emulator
```

### You may want C# code to generate connection string

_Note:_ No need to modify the secret, it was hardcoded in container.

```
static string GenerateConnStr(string ip = "127.0.0.1", int blobport = 10000, int queueport = 10001, int tableport = 10002)
{
    return $"DefaultEndpointsProtocol=http;AccountName=devstoreaccount1;AccountKey=Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==;BlobEndpoint=http://{ip}:{blobport}/devstoreaccount1;TableEndpoint=http://{ip}:{tableport}/devstoreaccount1;QueueEndpoint=http://{ip}:{queueport}/devstoreaccount1;";
}
```

Connect to emulator

```
var cloudStorageAccount = CloudStorageAccount.Parse(GenerateConnStr());

// ...
```
