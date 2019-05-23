# Azure Storage Emulator Docker Image
<https://docs.microsoft.com/en-us/azure/storage/storage-use-emulator>

[![Build status](https://dev.azure.com/farmer1992/opensources/_apis/build/status/DockerBuild-AzureStorageEmulator)](https://dev.azure.com/farmer1992/opensources/_build/latest?definitionId=9)

## Usage 

```
docker run -p 10000:10000 -p 10001:10001 -p 10002:10002 microsoft/azure-storage-emulator
```

### You may want C# code to generate connection string

_Note:_ No need to modify the secret, it was hardcoded in container.

Raw string
```
DefaultEndpointsProtocol=http;AccountName=devstoreaccount1;AccountKey=Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==;BlobEndpoint=http://127.0.0.1:10000/devstoreaccount1;TableEndpoint=http://127.0.0.1:10002/devstoreaccount1;QueueEndpoint=http://127.0.0.1:10001/devstoreaccount1;
```

C# 

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
