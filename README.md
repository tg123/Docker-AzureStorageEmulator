# Azure Storage Emulator Docker Image
<https://docs.microsoft.com/en-us/azure/storage/storage-use-emulator>

![Docker Build](https://farmer1992.visualstudio.com/_apis/public/build/definitions/3686302e-40e0-495b-a6f8-f2926767661b/9/badge)

## Usage 

```
docker run farmer1992/azure-storage-emulator
```

_NOTE_: you should use container ip to access the service or from different host when use port mapping due to WinNAT limitation <https://blogs.technet.microsoft.com/virtualization/2016/05/25/windows-nat-winnat-capabilities-and-limitations/>


### You may want C# code to generate connection string

```
static string GenerateConnStr(string ip = "127.0.0.1", int blobport = 10000, int queueport = 10001, int tableport = 10002)
{
    return $"DefaultEndpointsProtocol=http;AccountName=devstoreaccount1;AccountKey=Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==;BlobEndpoint=http://{ip}:{blobport}/devstoreaccount1;TableEndpoint=http://{ip}:{tableport}/devstoreaccount1;QueueEndpoint=http://{ip}:{queueport}/devstoreaccount1;";
}
```

Connect to emulator

```
var cloudStorageAccount = CloudStorageAccount.Parse(GenerateConnStr("container ip"));

// ...
```
