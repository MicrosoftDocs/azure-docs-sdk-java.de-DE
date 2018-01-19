---
uid: com.microsoft.azure.management.compute._virtual_machine
summary: *content
---

<span data-ttu-id="7a762-102">Der folgende Code veranschaulicht, wie die Java-SDKS fluent-Syntax zum Erstellen eines neuen [Standard D3](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-windows-sizes/#d-series) virtuellen Linux-Computer ausgeführten 16.04 Ubuntu Server im Rechenzentrum Osten der USA.</span><span class="sxs-lookup"><span data-stu-id="7a762-102">The code below demonstrates how to use the Java SDK's fluent syntax to create a new [Standard D3](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-windows-sizes/#d-series) Linux Virtual Machine running Ubuntu 16.04 server in the Eastern US data center.</span></span>

```java
Azure azure = Azure.authenticate(propertiesFile).withDefaultSubscription();
System.out.println("Creating a Linux VM");

VirtualMachine linuxVM = azure.virtualMachines().define("myLinuxVM")
        .withRegion(Region.US_EAST)
        .withNewResourceGroup("myResourceGroup")
        .withNewPrimaryNetwork("10.0.0.0/28")
        .withPrimaryPrivateIpAddressDynamic()
        .withNewPrimaryPublicIpAddress("mylinuxvmdns")
        .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
        .withRootUserName("tirekicker")
        .withSsh("your-ssh-key")
        .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
        .create();

System.out.println("Created a Linux VM: " + linuxVM.id());
```

---
uid: com.microsoft.azure.management.compute._virtual_machine.computerName()
summary: Ruft den Namen des virtuellen Computers ab.
---

---
uid: com.microsoft.azure.management.compute._virtual_machine.dataDisks()
summary: 'Ruft die Liste der Datenträger, die mit dem virtuellen Computer angefügt sind.'
---

---
uid: com.microsoft.azure.management.compute._virtual_machine.extensions()
summary: 'Ruft die Erweiterungen, die auf dem virtuellen Computer installiert sind.'
---

---
uid: com.microsoft.azure.management.compute._virtual_machine.getPrimaryPublicIpAddressId()
summary: Ruft den Bezeichner der öffentlichen IP-Adresse primären Netzwerkschnittstelle des virtuellen Computers zugeordnet.
---

---
uid: com.microsoft.azure.management.compute._virtual_machine.licenseType()
summary: Ruft den Lizenztyp des virtuellen Computers ab.
---

---
uid: com.microsoft.azure.management.compute._virtual_machine.osDiskCachingType()
summary: Ruft den Zwischenspeichern des Betriebssystem-Datenträgers ab.
---

---
uid: com.microsoft.azure.management.compute._virtual_machine.osDiskSize()
summary: Ruft die Größe des Betriebssystem-Datenträgers ab.
---

---
uid: com.microsoft.azure.management.compute._virtual_machine.osDiskVhdUri()
summary: 'Ruft den URI der virtuellen Festplatte, die das Betriebssystem enthält.'
---

---
uid: com.microsoft.azure.management.compute._virtual_machine.osType()
summary: Ruft den Typ des Betriebssystems ab.
---

---
uid: com.microsoft.azure.management.compute._virtual_machine.plan()
summary: Ruft den Plan für das Image des virtuellen Computers ab.
---

---
uid: com.microsoft.azure.management.compute._virtual_machine.powerState()
summary: Ruft den Energiezustand des virtuellen Computers ab.
---

---
uid: com.microsoft.azure.management.compute._virtual_machine.provisioningState()
summary: Ruft den Prrovisioning-Zustand des virtuellen Computers ab.
---

---
uid: com.microsoft.azure.management.compute._virtual_machine.size()
summary: Ruft die Größe des virtuellen Computers ab.
---

---
uid: com.microsoft.azure.management.compute._virtual_machine.vmId()
summary: Ruft den Bezeichner des virtuellen Computers ab.
---