# Install-VCFCertificate

## Synopsis

Installs the signed certificates for all components associated with the given workload domain, or an ESXi Host or for each ESXi host in a given cluster.

## Syntax

### Installing Certificates for a Workload Domain

```powershell
Install-VCFCertificate [-sddcManager] [-server] <String> [-user] <String> [-pass] <String> [-workloadDomain] <String> [<CommonParameters>]
```

### Installing Certificates ESXi Hosts in a Cluster

```powershell
Install-VCFCertificate [-esxi] [-server] <String> [-user] <String> [-pass] <String> [-domain] <String> [-cluster] <String> [-certificateDirectory] <String> [-certificateFileExt] <String> [[-timeout] <String>] [<CommonParameters>]
```

### Installing a Certificate for an ESXi Host

```powershell
Install-VCFCertificate [-esxi] [-server] <String> [-user] <String> [-pass] <String> [-domain] <String> [-esxiFqdn] <String> [-certificateDirectory] <String> [-certificateFileExt] <String> [[-timeout] <String>] [<CommonParameters>]
```

## Description

The `Install-VCFCertificate` will install the signed certificates for all components associated with the given workload domain when used with the `-sddcManager` switch.

The `Install-VCFCertificate` will replace the certificate for an ESXi host or for each ESXi host in a cluster when used with the `-esxi` switch.

When used with the `-esxi` switch, this cmdlet:

- You must provide the directory containing the signed certificate files.
- Certificate names should be in format `<FQDN>.crt` (_e.g._, `sfo01-m01-esx01.sfo.rainpole.io.crt`.)
- The workflow will put the ESXi host in maintenance mode with full data migration, disconnect the ESXi host from the vCenter Server, replace the certificate, restart the ESXi host, and the exit maintenance mode once the ESXi host is online.

## Examples

### Example 1

```powershell
Install-VCFCertificate -sddcManager -server sfo-vcf01.sfo.rainpole.io -user administrator@vsphere.local -pass VMw@re1! -workloadDomain sfo-w01
```

This example will connect to SDDC Manager to install the signed certificates for a given workload domain.

### Example 2

```powershell
Install-VCFCertificate -esxi -server sfo-vcf01.sfo.rainpole.io -user administrator@vsphere.local -pass VMw@re1! -domain sfo-m01 -esxiFqdn sfo01-m01-esx01.sfo.rainpole.io -certificateDirectory F:\certificates -certificateFileExt ".cer"
```

This example will install the certificate to the ESXi host sfo01-m01-esx01.sfo.rainpole.io in domain sfo-m01 from the provided path.

### Example 3

```powershell
Install-VCFCertificate -esxi -server sfo-vcf01.sfo.rainpole.io -user <administrator@vsphere.local> -pass VMw@re1! -domain sfo-m01 -cluster sfo-m01-cl01 -certificateDirectory F:\certificates -certificateFileExt ".cer"
```

This example will install certificates for each ESXi host in cluster sfo-m01-cl01 in workload domain sfo-m01 from the provided path.

## Parameters

### -esxi

Switch to indicate that the certificate is to be installed on an ESXi host.

```yaml
Type: SwitchParameter
Parameter Sets: (esxi)
Aliases:

Required: True
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -sddcManager

Switch to indicate that the certificate is to be installed for all components associated with the given workload domain, excluding ESXi hosts.

```yaml
Type: SwitchParameter
Parameter Sets: (sddcManager)
Aliases:

Required: True
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -server

The fully qualified domain name of the SDDC Manager instance.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -user

The username to authenticate to the SDDC Manager instance.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -pass

The password to authenticate to the SDDC Manager instance.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -domain

The name of the workload domain in which the certificate is requested to be installed or where the ESXi host is located.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -cluster

The name of the cluster in which the ESXi host is located.

```yaml
Type: String
Parameter Sets: (esxi)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -esxiFqdn

The fully qualified domain name of the ESXi host.

```yaml
Type: String
Parameter Sets: (esxi)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -certificateDirectory

The directory containing the signed certificate files.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -certificateFileExt

The file extension of the certificate files.
One of ".crt", ".cer", ".pem", ".p7b", or ".p7c".

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -timeout

The timeout in seconds for putting the ESXi host in maintenance mode.
Default is 18000 seconds (5 hours).

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: 18000
Accept pipeline input: False
Accept wildcard characters: False
```

### Common Parameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).
