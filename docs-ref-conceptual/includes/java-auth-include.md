Erstellen Sie eine [Authentifizierungsdatei](../java-sdk-azure-authenticate.md#mgmt-file), und exportieren Sie die Umgebungsvariable `AZURE_AUTH_LOCATION` in der Befehlszeile mit dem vollständigen Pfad zur Datei.

```bash
export AZURE_AUTH_LOCATION=/Users/raisa/azure.auth
```

Mit der Authentifizierungsdatei wird das Eingangspunktobjekt `Azure` konfiguriert, das von den Verwaltungsbibliotheken zum Definieren, Erstellen und Konfigurieren von Azure-Ressourcen verwendet wird.

```java
// pull in the location of the security file from the environment 
final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));

Azure azure = Azure
        .configure()
        .withLogLevel(LogLevel.NONE)
        .authenticate(credFile)
        .withDefaultSubscription();
```

[Weitere Informationen](../java-sdk-azure-authenticate.md#mgmt-auth) zu Authentifizierungsoptionen bei Verwendung der Azure-Verwaltungsbibliotheken für Java.