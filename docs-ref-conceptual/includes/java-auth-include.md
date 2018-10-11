<span data-ttu-id="23f34-101">Erstellen Sie eine [Authentifizierungsdatei](../java-sdk-azure-authenticate.md#mgmt-file), und exportieren Sie die Umgebungsvariable `AZURE_AUTH_LOCATION` in der Befehlszeile mit dem vollständigen Pfad zur Datei.</span><span class="sxs-lookup"><span data-stu-id="23f34-101">Create an [authentication file](../java-sdk-azure-authenticate.md#mgmt-file) and export an environment variable `AZURE_AUTH_LOCATION` on the command line with the full path to the file.</span></span>

```bash
export AZURE_AUTH_LOCATION=/Users/raisa/azure.auth
```

<span data-ttu-id="23f34-102">Mit der Authentifizierungsdatei wird das Eingangspunktobjekt `Azure` konfiguriert, das von den Verwaltungsbibliotheken zum Definieren, Erstellen und Konfigurieren von Azure-Ressourcen verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="23f34-102">The authentication file is used to configure the entry point `Azure` object used by the management libraries to define, create, and configure Azure resources.</span></span>

```java
// pull in the location of the security file from the environment 
final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));

Azure azure = Azure
        .configure()
        .withLogLevel(LogLevel.NONE)
        .authenticate(credFile)
        .withDefaultSubscription();
```

<span data-ttu-id="23f34-103">[Weitere Informationen](../java-sdk-azure-authenticate.md#mgmt-auth) zu Authentifizierungsoptionen bei Verwendung der Azure-Verwaltungsbibliotheken für Java.</span><span class="sxs-lookup"><span data-stu-id="23f34-103">[Learn more](../java-sdk-azure-authenticate.md#mgmt-auth) about authentication options when using the Azure management libraries for Java.</span></span>