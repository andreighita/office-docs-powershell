---
external help file: Microsoft.Exchange.RecordsandEdge-Help.xml
applicable: Exchange Server 2016, Exchange Server 2019, Exchange Online
title: Restore-RecoverableItems
schema: 2.0.0
author: chrisda
ms.author: chrisda
ms.reviewer:
monikerRange: "exchserver-ps-2016 || exchserver-ps-2019 || exchonline-ps" 
---

# Restore-RecoverableItems

## SYNOPSIS
This cmdlet is available in on-premises Exchange and in the cloud-based service. Some parameters and settings may be exclusive to one environment or the other.

Use the Restore-RecoverableItems items cmdlet to restore deleted items in the Recoverable Items folder in mailboxes. You use the Get-RecoverableItems cmdlet to find the deleted items to recover.

For information about the parameter sets in the Syntax section below, see Exchange cmdlet syntax (https://technet.microsoft.com/library/bb123552.aspx).

## SYNTAX

```
Restore-RecoverableItems -Identity <GeneralMailboxOrMailUserIdParameter> [-EntryID <String>] [-FilterEndTime <DateTime>] [-FilterItemType <String>] [-FilterStartTime <DateTime>] [-LastParentFolderID <String>] [-ResultSize <Unlimited>] [-SourceFolder <DeletedItems | RecoverableItems | Purgeditems>] [-SubjectContains <String>] [<CommonParameters>]
```

## DESCRIPTION
Items are restored to the original folder location if the information is available for the item. If the information can't be found, the item is restored to the default folder for the item type (Inbox for messages, Calendar for meetings and appointments, etc.).

You need to be assigned permissions before you can run this cmdlet. Although this topic lists all parameters for the cmdlet, you may not have access to some parameters if they're not included in the permissions assigned to you. To find the permissions required to run any cmdlet or parameter in your organization, see Find the permissions required to run any Exchange cmdlet (https://technet.microsoft.com/library/mt432940.aspx).

## EXAMPLES

### -------------------------- Example 1 --------------------------
```
Restore-RecoverableItems -Identity laura@contoso.com -FilterItemType IPM.Note -SubjectContains "FY17 Accounting" -FilterStartTime "2/1/2018 12:00:00 AM" -FilterEndTime "2/5/2018 11:59:59 PM"
```

After using the Get-RecoverableItems cmdlet to verify the existence of the item, this example restores the specified deleted item from the specified mailbox:

- Mailbox: laura@contoso.com

- Item type: Email message

- Message subject: FY17 Accounting

- Location: Recoverable Items\Deletions

- Date range: 2/1/2018 to 2/5/2018

### -------------------------- Example 2 --------------------------
```
$mailboxes = Import-CSV "C:\My Documents\RestoreMessage.csv"; $mailboxes | foreach {Restore-RecoverableItems -Identity $_.SMTPAddress -SubjectContains Project X" -SourceFolder DeletedItems -FilterItemType IPM.Note}
```

This example restores the deleted email message "Project X" for the mailboxes that are specified in the comma-separated value (CSV) file C:\\My Documents\\RestoreMessage.csv. The CSV file uses the header value SMTPAddress, and contains the email address of each mailbox on a separate line like this:

SMTPAddress

chris@contoso.com

michelle@contoso.com

laura@contoso.com

julia@contoso.com

The first command reads the CSV file and writes the information to the variable $mailboxes. The second command restores the specified message from the Deleted Items folder in those mailboxes.

## PARAMETERS

### -Identity
The Identity parameter specifies the mailbox that contains the Recoverable Items folder where you want to restore items from. You can use any value that uniquely identifies the mailbox.

For example:

- Name

- Display name

- Alias

- Distinguished name (DN)

- Canonical DN

- \<domain name>\<account name>

- Email address

- GUID

- LegacyExchangeDN 

- SamAccountName 

- User ID or user principal name (UPN)

```yaml
Type: GeneralMailboxOrMailUserIdParameter
Parameter Sets: (All)
Aliases:
Applicable: Exchange Server 2016, Exchange Server 2019, Exchange Online
Required: True
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -EntryID
The EntryID parameter specifies the deleted item that you want to restore. The EntryID value for the deleted item is unique in the mailbox.

You can find the EntryID for specific items by using other search filters on the Get-RecoverableItems cmdlet (subject, date range, etc.).

```yaml
Type: String
Parameter Sets: (All)
Aliases:
Applicable: Exchange Server 2016, Exchange Online
Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -FilterEndTime
The FilterEndTime specifies the end date/time of the date range.

Use the short date format that's defined in the Regional Options settings on the computer where you're running the command. For example, if the computer is configured to use the short date format mm/dd/yyyy, enter 09/01/2018 to specify September 1, 2018. You can enter the date only, or you can enter the date and time of day. If you enter the date and time of day, enclose the value in quotation marks ("), for example, "09/01/2018 5:00 PM".

```yaml
Type: DateTime
Parameter Sets: (All)
Aliases:
Applicable: Exchange Server 2016, Exchange Server 2019, Exchange Online
Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -FilterItemType
The FilterItemType parameter filters the results by the specified MessageClass (ItemClass) property value of the deleted item. For example:

- IPM.Appointment (Meetings and appointments)

- IPM.Contact

- IPM.File

- IPM.Note

- IPM.Task

```yaml
Type: String
Parameter Sets: (All)
Aliases:
Applicable: Exchange Online
Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -FilterStartTime
The FilterStartTime specifies the start date/time of the date range.

Use the short date format that's defined in the Regional Options settings on the computer where you're running the command. For example, if the computer is configured to use the short date format mm/dd/yyyy, enter 09/01/2018 to specify September 1, 2018. You can enter the date only, or you can enter the date and time of day. If you enter the date and time of day, enclose the value in quotation marks ("), for example, "09/01/2018 5:00 PM".

```yaml
Type: DateTime
Parameter Sets: (All)
Aliases:
Applicable: Exchange Server 2016, Exchange Server 2019, Exchange Online
Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -LastParentFolderID
The LastParentFolderID parameter specifies the FolderID value of the item before it was deleted. For example, 53B93149989CA54DBC9702AE619B9CCA000062CE9397.

```yaml
Type: String
Parameter Sets: (All)
Aliases:
Applicable: Exchange Online
Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ResultSize
The ResultSize parameter specifies the maximum number of results to return. If you want to return all requests that match the query, use unlimited for the value of this parameter. The default value is 1000.

```yaml
Type: Unlimited
Parameter Sets: (All)
Aliases:
Applicable: Exchange Server 2016, Exchange Server 2019, Exchange Online
Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -SourceFolder
The SourceFolder parameter specifies the folder in the mailbox to search for deleted items. Valid values are:

- DeletedItems: The Deleted Items folder.

- RecoverableItems: Recoverable items that have been deleted from the Deleted Items folder.

- Purgeditems: If either Litigation Hold or single item recovery is enabled on the mailbox, this folder contains all items that are hard deleted. This folder isn't visible to end users.

If you don't use this parameter, the command will search all locations.

```yaml
Type: DeletedItems | RecoverableItems
Parameter Sets: (All)
Aliases:
Accepted values: DeletedItems, RecoverableItems
Applicable: Exchange Online
Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -SubjectContains
The SubjectContains parameter filters the items by the specified text value in the Subject field. If the value contains spaces, enclose the value in quotation marks (").

```yaml
Type: String
Parameter Sets: (All)
Aliases:
Applicable: Exchange Server 2016, Exchange Server 2019, Exchange Online
Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see about_CommonParameters (https://go.microsoft.com/fwlink/p/?LinkID=113216).

## INPUTS

###  
To see the input types that this cmdlet accepts, see Cmdlet Input and Output Types (https://go.microsoft.com/fwlink/p/?LinkId=616387). If the Input Type field for a cmdlet is blank, the cmdlet doesn't accept input data.

## OUTPUTS

###  
To see the return types, which are also known as output types, that this cmdlet accepts, see Cmdlet Input and Output Types (https://go.microsoft.com/fwlink/p/?LinkId=616387). If the Output Type field is blank, the cmdlet doesn't return data.

## NOTES

## RELATED LINKS

[Online Version](https://docs.microsoft.com/powershell/module/exchange/mailboxes/Restore-RecoverableItems)
