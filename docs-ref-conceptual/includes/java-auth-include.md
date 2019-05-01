---
ms.openlocfilehash: 0a9b06932baa51c3cf003a4485a3a25261ffe91d
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2019
ms.locfileid: "61592502"
---
<span data-ttu-id="336b9-101">Erstellen Sie eine [Authentifizierungsdatei](../java-sdk-azure-authenticate.md#mgmt-file), und exportieren Sie die Umgebungsvariable `AZURE_AUTH_LOCATION` in der Befehlszeile mit dem vollständigen Pfad zur Datei.</span><span class="sxs-lookup"><span data-stu-id="336b9-101">Create an [authentication file](../java-sdk-azure-authenticate.md#mgmt-file) and export an environment variable `AZURE_AUTH_LOCATION` on the command line with the full path to the file.</span></span>

```bash
export AZURE_AUTH_LOCATION=/Users/raisa/azure.auth
```

<span data-ttu-id="336b9-102">Mit der Authentifizierungsdatei wird das Eingangspunktobjekt `Azure` konfiguriert, das von den Verwaltungsbibliotheken zum Definieren, Erstellen und Konfigurieren von Azure-Ressourcen verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="336b9-102">The authentication file is used to configure the entry point `Azure` object used by the management libraries to define, create, and configure Azure resources.</span></span>

```java
// pull in the location of the security file from the environment 
final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));

Azure azure = Azure
        .configure()
        .withLogLevel(LogLevel.NONE)
        .authenticate(credFile)
        .withDefaultSubscription();
```

<span data-ttu-id="336b9-103">[Weitere Informationen](../java-sdk-azure-authenticate.md#mgmt-auth) zu Authentifizierungsoptionen bei Verwendung der Azure-Verwaltungsbibliotheken für Java.</span><span class="sxs-lookup"><span data-stu-id="336b9-103">[Learn more](../java-sdk-azure-authenticate.md#mgmt-auth) about authentication options when using the Azure management libraries for Java.</span></span>