﻿---
title: Set-CsSlaConfiguration
TOCTitle: Set-CsSlaConfiguration
ms:assetid: e701759e-14e1-4017-b46c-3976eba3e561
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Mt703202(v=OCS.15)
ms:contentKeyID: 72808513
ms.date: 04/12/2016
mtps_version: v=OCS.15
---

<div data-xmlns="http://www.w3.org/1999/xhtml">

<div class="topic" data-xmlns="http://www.w3.org/1999/xhtml" data-msxsl="urn:schemas-microsoft-com:xslt" data-cs="http://msdn.microsoft.com/en-us/">

<div data-asp="http://msdn2.microsoft.com/asp">

# Set-CsSlaConfiguration

</div>

<div id="mainSection">

<div id="mainBody">

<span> </span>

_**Topic Last Modified:** 2016-04-12_

Use the **Set-CsSlaConfiguration** cmdlet to create or modify a shared number in Shared Line Appearance (SLA). A shared number in SLA is an Enterprise Voice user that is capable of receiving multiple calls at a time and forwarding them to its delegates, who answer the call.

<div>

## Syntax

    Set-CsSlaConfiguration -Identity <UserIdParameter> [-BusyOption <Forward | BusyOnBusy | Voicemail>] [-Confirm [<SwitchParameter>]] [-MaxNumberOfCalls <UInt32>] [-MissedCallForwardTarget <Uri>] [-MissedCallOption <Disconnect | Forward | BusySignal>] [-PassThru <SwitchParameter>] [-Target <Uri>] [-WhatIf [<SwitchParameter>]]

</div>

<span id="Examples"></span>

<div>

## Examples

<div>

## Example 1

This example configures SLA for a user identified as “emergency” that can accept at max 3 calls at a time. Note that “emergency” is a valid enterprise voice enabled Skype for Business (SfB) user. BusyOption is required if SLA is being setup for the first time.

    Set-CsSlaConfiguration -Identity emergency -MaxNumberOfCalls 3 -BusyOption BusyOnBusy

</div>

<div>

## Example 2

This example configures SLA for a user identified as “emergency” to forward calls to “sla\_forward\_number” when all lines are busy.

``` 
Set-CsSlaConfiguration -Identity emergency -MaxNumberOfCalls 3 -BusyOption Forward -Target sip:sla_forward_number@contosohealth.com  
```

</div>

<div>

## Example 3

This example configures SLA for a user identified as “emergency” to transfer to voice mail when all lines are busy.

    Set-CsSlaConfiguration -Identity emergency -MaxNumberOfCalls 3 -BusyOption Voicemail

</div>

</div>

<span id="DetailedDescription"></span>

<div>

## Detailed Description

SLA is a feature in Skype for Business (SfB) for handling multiple calls on a specific number called a shared number. SLA can configure any enterprise voice enabled SfB user as a shared number with multiple lines to respond to multiple calls. The calls are not actually received on the shared number, instead they are forwarded to users that act as delegates for the shared number. Any one of the delegates can pick up the call while the rest of the delegates get a notification on their phone about who picked up the call and which line has become busy as a result. Both the number of lines and the delegates are configurable for a shared number in SLA. In addition, advanced options such as BusyOption (what happens in a situation when all lines are busy) and MissedCallOption (the case in which none of the delegates pick up a call) etc. can also be configured for a shared number.

The Set-CsSlaConfiguration cmdlet provides a way to configure a shared number.

<div>


> [!NOTE]
> Logging in with the account created for the SLA number is not supported. Using the SLA number account with any device or Desktop Client can result in unpredictable behavior. It is not necessary to use that account for the Shared Line Appearance feature to function.



</div>

By default, members of the RTCUniversalServerAdmins group are authorized to run the **Set-CsSlaConfiguration** cmdlet. To return a list of all the role-based access control (RBAC) roles this cmdlet has been assigned to (including any custom RBAC roles you have created yourself), run the following command from the Windows PowerShell prompt:

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Set-CsSlaConfiguration"}

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
<td><p><em>Identity</em></p></td>
<td><p>Required</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>Indicates the identity of the Enterprise Voice user whose shared number information will be created or modified.</p>
<p>UNRESOLVED_TOKENBLOCK_VAL(PS_PD_User_Updated_Specification)</p></td>
</tr>
<tr class="even">
<td><p><em>BusyOption</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.SlaBusyOption</p></td>
<td><p>Specifies the action to take when all lines are busy. The valid values for the option are “Forward”, ”BusyOnBusy”, or “Voicemail”. The default is “BusyOnBusy”.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Prompts you for confirmation before executing the command.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxNumberOfCalls</em></p></td>
<td><p>Optional</p></td>
<td><p>System.UInt32</p></td>
<td><p>Specifies the maximum number of calls the shared number can receive.</p></td>
</tr>
<tr class="odd">
<td><p><em>MissedCallForwardTarget</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Uri</p></td>
<td><p>Specifies the forwarding target if <em>MissedCallOption</em> is set to “Forward”. <em>MissedCallForwardTarget</em> should be set to a valid SIP Uri. If the PSTN number needs to be specified, it should be prefixed with “tel:”. For example, “tel:+2504395”.</p></td>
</tr>
<tr class="even">
<td><p><em>MissedCallOption</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.SlaUserMissedCallOption</p></td>
<td><p>Specifies the action to take when none of the delegates picks up the call. The valid values for the option are “Disconnect”, “Forward”, or “BusySignal”. The default is “Disconnect”.</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>UNRESOLVED_TOKEN_VAL(PS_PD_Passthru_Generic_CurrentObjects)</p></td>
</tr>
<tr class="even">
<td><p><em>Target</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Uri</p></td>
<td><p>Specifies the forwarding target if <em>BusyOption</em> is set to “Forward”. <em>Target</em> should be set to a valid SIP Uri. If the PSTN number needs to be specified, it should be prefixed with “tel:”, “tel:+2504395”.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Describes what would happen if you executed the command without actually executing the command.</p></td>
</tr>
</tbody>
</table>


</div>

<span id="InputTypes"></span>

<div>

## Input Types

The **Set-CsSlaConfiguration** cmdlet accepts a pipelined object representing a user account that has been enabled for Skype for Business Server 2015.

</div>

<span id="ReturnTypes"></span>

<div>

## Return Types

The **Set-CsSlaConfiguration** cmdlet returns an instance of the Microsoft.Rtc.Management.SlaConfiguration object.

</div>

</div>

<span> </span>

</div>

</div>

</div>

