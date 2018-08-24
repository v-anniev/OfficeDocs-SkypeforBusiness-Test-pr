﻿---
title: Enable-CsAdDomain
TOCTitle: Enable-CsAdDomain
ms:assetid: a39768de-51ae-45e8-b6b7-441b5da0b3b2
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Gg412764(v=OCS.15)
ms:contentKeyID: 48185042
ms.date: 07/07/2014
mtps_version: v=OCS.15
---

<div data-xmlns="http://www.w3.org/1999/xhtml">

<div class="topic" data-xmlns="http://www.w3.org/1999/xhtml" data-msxsl="urn:schemas-microsoft-com:xslt" data-cs="http://msdn.microsoft.com/en-us/">

<div data-asp="http://msdn2.microsoft.com/asp">

# Enable-CsAdDomain

</div>

<div id="mainSection">

<div id="mainBody">

<span> </span>

_**Topic Last Modified:** 2014-07-01_

Modifies the security settings on the universal groups created during forest preparation. These modifications provide the permissions needed to host and manage users enabled for Lync Server within the domain. This cmdlet was introduced in Lync Server 2010.

<div>

## Syntax

    Enable-CsAdDomain [-Confirm [<SwitchParameter>]] [-CrossForest <SwitchParameter>] [-Domain <Fqdn>] [-DomainController <Fqdn>] [-Force <SwitchParameter>] [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] [-Report <String>] [-SkipPrepareCheck <$true | $false>] [-WhatIf [<SwitchParameter>]]

</div>

<div>

## Examples

<div>

## EXAMPLE 1

The command shown in Example 1 prepares the local domain for the installation of Lync Server.

    Enable-CsAdDomain

</div>

<div>

## EXAMPLE 2

Example 2 prepares the domain asia.litwareinc.com for the installation of Lync Server.

    Enable-CsAdDomain -Domain asia.litwareinc.com

</div>

</div>

<div>

## Detailed Description

Before you can install Lync Server in a domain, that domain must be correctly prepared, a process that includes extending the Active Directory schema to allow for the addition of attributes specific to Lync Server as well as assigning the required Access Control Entries to the universal groups needed for managing and operating Lync Server. Domain preparation is typically carried out through the Lync Server Setup Wizard. However, administrators can also perform domain preparation by running the **Enable-CsAdDomain** cmdlet.

After the **Enable-CsAdDomain** cmdlet finishes running, you can use the **Get-CsAdDomain** cmdlet to verify that the domain is ready for the next step in the installation process.



> [!NOTE]
> If you receive the following error, “Cannot find the object ‘CrossRef’ in Active Directory” while running tasks to prepare a child domain of a single-forest environment with multiple domains, you may have to manually add the RTCComponentUniversalServices group from the parent domain to the Windows Authorization Access group in the child domain.



This cmdlet carries out tasks similar to those carried out by the following Microsoft Office Communications Server 2007 R2 command:

Lcscmd.exe /domain /action:DomainPrep

Who can run this cmdlet: You must be a domain administrator in order to run the **Enable-CsAdDomain** cmdlet locally.

</div>

<div>

## Parameters


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Parameter</th>
<th>Required</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Prompts you for confirmation before executing the command.</p></td>
</tr>
<tr class="even">
<td><p><em>CrossForest</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>If present, indicates that domain preparation is taking place in a domain in a different forest. This parameter is not required if the domain being enabled is in the same forest as the computer where the command is being run.</p></td>
</tr>
<tr class="odd">
<td><p><em>Domain</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Fully qualified domain name (FQDN) of the domain where domain preparation is to take place (for example, -Domain asia.litwareinc.com). If this parameter is not included, domain preparation will take place on the local domain.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Enables administrators to specify the FQDN of the domain controller to be used when running the <strong>Enable-CsAdDomain</strong> cmdlet. If not specified, the cmdlet will use the first available domain controller.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Suppresses the display of any non-fatal error message that might arise when running the command.</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalCatalog</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>FQDN of a global catalog server in your domain. This parameter is not required if you are running the <strong>Enable-CsAdDomain</strong> cmdlet on a computer with an account in your domain.</p></td>
</tr>
<tr class="odd">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>FQDN of a domain controller where global settings are stored. If global settings are stored in the System container in Active Directory Domain Services, then this parameter must point to the root domain controller. If global settings are stored in the Configuration container then any domain controller can be used and this parameter can be omitted.</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>Enables you to specify a file path for the log file created when the cmdlet runs. For example: -Report &quot;C:\Logs\DomainPrep.html&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>SkipPrepareCheck</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Boolean</p></td>
<td><p>If set to True ($True), then the <strong>Enable-CsAdDomain</strong> cmdlet will skip its initial preparation check.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Describes what would happen if you executed the command without actually executing the command.</p></td>
</tr>
</tbody>
</table>


</div>

<div>

## Input Types

None. The **Enable-CsAdDomain** cmdlet does not accept pipelined input.

</div>

<div>

## Return Types

None.

</div>

<div>

## See Also


[Disable-CsAdDomain](disable-csaddomain.md)  
[Get-CsAdDomain](get-csaddomain.md)  
  

</div>

</div>

<span> </span>

</div>

</div>

</div>

