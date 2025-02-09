---
title: Assign conditional-based values and rules
titleSuffix: Azure DevOps & TFS
description: Syntax and usage for WHEN, WHENNOT, WHENCHANGED, and WHENNOTCHANGED elements that define conditional rules and values
ms.technology: devops-agile
ms.custom: process
ms.assetid: 7975a8a3-6fa1-43c1-b32b-0bbb9bb336af
ms.author: kaelli
author: KathrynEE
ms.topic: reference
monikerRange: '< azure-devops'
ms.date: 01/20/2017
---

# Assign conditional-based values and rules

[!INCLUDE [temp](../../includes/customization-phase-0-and-1-plus-version-header.md)]

You can define rules that are run conditionally by using the **WHEN**, **WHENNOT**, **WHENCHANGED**, and **WHENNOTCHANGED** elements. You use these rules to define which elements are run when the defined clause is `True`. You can define conditions that are based on what value is assigned to a specific field or whether a user modifies a specific field. For example, you can create a dependent pick list to provide detailed security or custom behavior.  

Field conditions are additional elements that you list inside a `FIELD` (Definition) element or the `FIELD` (Workflow) element. For more information about these elements, see [FIELD (Definition) element reference](field-definition-element-reference.md) and [FIELD (Workflow)](field-workflow-element-reference.md).  

 The following code is a simple example of the **WHEN** clause:  


> [!div class="tabbedCodeSnippets"]
> ```XML
> <FIELD  . . .  > 
> <WHEN field="referenceName" value="yyy">  
> </FIELD>
> ```  

 This clause means that anything within this FIELD element is applicable as long as the field `refname` has the value "yyy". The field must be a valid field reference name. For more information, see [Naming conventions for work item tracking objects](../../organizations/settings/naming-restrictions.md#ProjectNames).  

> [!NOTE]  
>  The value attribute is case-insensitive. Therefore, if the field reference name holds "YYY", matches include the values "yyy" and "YYY".  

<a name="Syntax"></a>   

##  Syntax structure for conditional elements  

The following table describes conditional rules that you can specify as child elements of the `FIELD` (Definition) element or `FIELD` (Workflow) element. These elements accept one or more of the following attributes:  

-   `field`: A string that describes the field. Must contain 1 to 255 characters.   
-   `value`: When the specified field has this value, the rules in the `WHEN` and `WHENNOT` elements are applied to the current field.    

:::row:::
   :::column span="1":::
   **Element**
   :::column-end:::
   :::column span="2":::
   **Syntax**
   :::column-end:::
   :::column span="1":::
   **Description**
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="1":::
   **WHEN**

   :::column-end:::
   :::column span="2":::
   
   ```
   <WHEN field="fieldReferenceName" value="value">
       <ALLOWEDVALUES> . . . </ALLOWEDVALUES>
       <ALLOWEXISTINGVALUE> . . . <ALLOWEXISTINGVALUE>
       <CANNOTLOSEVALUE> . . . </CANNOTLOSEVALUE>
       <COPY> . . . </COPY>
       <DEFAULT> . . . </DEFAULT>
       <EMPTY> . . . </EMPTY>
       <FROZEN> . . . </FROZEN>
       <MATCH> . . . </MATCH>
       <NOTSAMEAS> . . . </NOTSAMEAS>
       <PROHIBITEDVALUES> . . . </PROHIBITEDVALUES>
       <READONLY> . . . </READONLY>
       <REQUIRED> . . . </REQUIRED>
       <SERVERDEFAULT> . . . </SERVERDEFAULT>
       <SUGGESTEDVALUES> . . . </SUGGESTEDVALUES>
       <VALIDUSER> . . . </VALIDUSER>
   </WHEN>
   ```
   :::column-end:::
   :::column span="1":::
   Specifies one or more rules to apply to the current field when another field has a specific value. The parent element defines the current field.  
   
   When the specified field has the specified value, the rules in this element are applied to the current field.

   :::column-end:::
:::row-end:::
:::row:::
   :::column span="1":::
   **WHENNOT**

   :::column-end:::
   :::column span="2":::
   
   ```
   <WHENNOT field="fieldReferenceName" value="value">
       <ALLOWEDVALUES> . . . </ALLOWEDVALUES>
       <ALLOWEXISTINGVALUE> . . . <ALLOWEXISTINGVALUE>
       <CANNOTLOSEVALUE> . . . </CANNOTLOSEVALUE>
       <COPY> . . . </COPY>
       <DEFAULT> . . . </DEFAULT>
       <EMPTY> . . . </EMPTY>
       <FROZEN> . . . </FROZEN>
       <MATCH> . . . </MATCH>
       <NOTSAMEAS> . . . </NOTSAMEAS>
       <PROHIBITEDVALUES> . . . </PROHIBITEDVALUES>
       <READONLY> . . . </READONLY>
       <REQUIRED> . . . </REQUIRED>
       <SERVERDEFAULT> . . . </SERVERDEFAULT><br/><SUGGESTEDVALUES> . . . </SUGGESTEDVALUES>
       <VALIDUSER> . . . </VALIDUSER>
   </WHENNOT>
   ```
   :::column-end:::
   :::column span="1":::
   Specifies a condition under which to apply one or more rules to the current field. The rules apply to the current field when the value of another field changes. The parent element defines the current field.  
   
   When the specified field does not contain the specified value, the rules in this element are applied to the current field.

   :::column-end:::
:::row-end:::
:::row:::
   :::column span="1":::
   **WHENCHANGED**

   :::column-end:::
   :::column span="2":::
   
   ```
   <WHENCHANGED field="fieldReferenceName" >
       <ALLOWEDVALUES> . . . </ALLOWEDVALUES>
       <ALLOWEXISTINGVALUE> . . . <ALLOWEXISTINGVALUE>
       <CANNOTLOSEVALUE> . . . </CANNOTLOSEVALUE>
       <COPY> . . . </COPY>
       <DEFAULT> . . . </DEFAULT>
       <EMPTY> . . . </EMPTY>
       <FROZEN> . . . </FROZEN>
       <MATCH> . . . </MATCH>
       <NOTSAMEAS> . . . </NOTSAMEAS>
       <PROHIBITEDVALUES> . . . </PROHIBITEDVALUES>
       <READONLY> . . . </READONLY>
       <REQUIRED> . . . </REQUIRED>
       <SERVERDEFAULT> . . . </SERVERDEFAULT>
       <SUGGESTEDVALUES> . . . </SUGGESTEDVALUES>
       <VALIDUSER> . . . </VALIDUSER>  
   </WHENCHANGED>
   ```
   :::column-end:::
   :::column span="1":::
   Specifies a condition under which to apply one or more rules to the current field. The rules apply to the current field when the value of another field is changed in a revision to a work item. The parent element defines the current field.

   :::column-end:::
:::row-end:::
:::row:::
   :::column span="1":::
   **WHENNOTCHANGED**

   :::column-end:::
   :::column span="2":::
   
   ```
   <WHENNOTCHANGED field="fieldReferenceName">
       <ALLOWEDVALUES> . . . </ALLOWEDVALUES>
       <ALLOWEXISTINGVALUE> . . . <ALLOWEXISTINGVALUE>
       <CANNOTLOSEVALUE> . . . </CANNOTLOSEVALUE>
       <COPY> . . . </COPY>
       <DEFAULT> . . . </DEFAULT>
       <EMPTY> . . . </EMPTY>
       <FROZEN> . . . </FROZEN>
       <MATCH> . . . </MATCH>
       <NOTSAMEAS> . . . </NOTSAMEAS>
       <PROHIBITEDVALUES> . . . </PROHIBITEDVALUES>
       <READONLY> . . . </READONLY>
       <REQUIRED> . . . </REQUIRED>
       <SERVERDEFAULT> . . . </SERVERDEFAULT>  
	   <SUGGESTEDVALUES> . . . </SUGGESTEDVALUES>
       <VALIDUSER> . . . </VALIDUSER>
   </WHENNOTCHANGED>
   ```
   :::column-end:::
   :::column span="1":::
   Specifies a condition under which to apply one or more rules to the current field. The rules apply to the current field when the value of another field is not changed in a revision to a work item. The parent element defines the current field.
   :::column-end:::
:::row-end:::


 The following table describes how each optional, conditional-based rule is applied to the parent field when the conditional clause that you specify by using a **WHEN**, **WHENNOT**, **WHENCHANGED**, or **WHENNOTCHANGED** element is true. For more information, see [Rules and rule evaluation](../../organizations/settings/work/rule-reference.md).  

|Element|Description|  
|-------------|-----------------|  
|[ALLOWEDVALUES](define-pick-lists.md)|The parent field must have a value that comes from the specified list of values.|  
|[ALLOWEXISTINGVALUE](define-pick-lists.md)|The value of the parent field that already exists will be allowed, even if it violates other rules. This element is not applicable if the value of the parent field is changed.|  
|[CANNOTLOSEVALUE](../../organizations/settings/work/rule-reference.md)|Users can change the value of the parent field to NULL, but they cannot change it to any other value.|  
|[COPY](define-default-copy-value-field.md)|The value of a third field is automatically copied into the parent field. You specify the third field in the **COPY** element.|  
|[DEFAULT](define-default-copy-value-field.md)|This element specifies the default value of the parent field.|  
|[EMPTY](../../organizations/settings/work/rule-reference.md)|The parent field must not contain a value.|  
|[FROZEN](../../organizations/settings/work/rule-reference.md)|The parent field is frozen. When a field is frozen, you can change its value to NULL, but you cannot change it to any other value.|  
|[MATCH](apply-pattern-matching-to-string-field.md)|The value of the parent field must match the pattern that you specify.|  
|[NOTSAMEAS](../../organizations/settings/work/rule-reference.md)|The value of the parent field cannot match the value of a third field. You specify the third field in the **NOTSAMEAS** element.|  
|[PROHIBITEDVALUES](define-pick-lists.md)|The parent field cannot contain any values in the enumerated list.|  
|[READONLY](../../organizations/settings/work/rule-reference.md)|The parent field is read-only.|  
|[REQUIRED](../../organizations/settings/work/rule-reference.md)|The parent field must contain a value that is not NULL.|  
|[SERVERDEFAULT](define-default-copy-value-field.md)|The parent field takes its value from the specified server component. The valid server components are **clock**, which is the time when the work item is updated, and **currentuser**, which is the identity of the user who updated the work item.|  
|[SUGGESTEDVALUES](define-pick-lists.md)|The enumerated list contains suggested values for the parent field.|  
|[VALIDUSER](../../organizations/settings/work/rule-reference.md)|Only the users whom you specify can modify the parent field.|  


<a name="DependentRequired"></a>   

##  Define a dependent required field  

You can specify that a field is required only when another field contains a specific value. In the following example, when a customer reports a bug, a customer severity must be specified. If the bug was not reported by a customer, a customer severity is not required.  

> [!div class="tabbedCodeSnippets"]
> ```XML
> <FIELD refname="MyCorp.Severity" name="Customer Severity" type="String">  
>        <ALLOWEDVALUES>  
>            <LISTITEM value="Blocking" />  
>            <LISTITEM value="Major" />  
>            <LISTITEM value="Minor" />  
>        </ALLOWEDVALUES>  
>        <WHEN field="MyCorp.CustomerReported" value="true">  
>            <REQUIRED />  
>        </WHEN>  
> </FIELD>  
> ```  



<a name="DependentPickList"></a> 

##  Define a conditional pick list  

The following example demonstrates a conditional pick list in which the allowed values for the Problem Type field are limited, based on whether the value of the ProblemCharacteristic field is set to Documentation.  

> [!div class="tabbedCodeSnippets"]
> ```XML
> <FIELD refname="MyCorp.ProblemType" name="Problem Type" type="String">  
>        <WHEN field="MyCorp.ProblemCharacteristic" value="Documentation">  
>            <ALLOWEDVALUES>  
>                <LISTITEM value="Spelling Error" />  
>                <LISTITEM value="Bad Format" />  
>                <LISTITEM value="Missing Info" />  
>            </ALLOWEDVALUES>  
>        </WHEN>  
> </FIELD>  
> ```  

<a name="WhenChanged"></a>  

##  Define a field when the user changes another field (WHENCHANGED)  

In the following example, when a user changes the value of the MyCorp.State field, the MyCorp.StateDate field is set to the current date and time, as the server clock shows.  

> [!div class="tabbedCodeSnippets"]
> ```XML
> <FIELD refname="MyCorp.StateDate" name="Date Of Last State Change" type="DateTime">  
>        <WHENCHANGED field="MyCorp.State">  
>            <COPY from="clock" />  
>        </WHENCHANGED>  
> </FIELD>   
> ```  

 In the following example, when a user changes the value of the MyCorp.State field, the value of the MyCorp.Status field is cleared.  

> [!div class="tabbedCodeSnippets"]
> ```XML  
> <!-- Clear the status field whenever someone changes the state -->  
> <FIELD refname="MyCorp.Status" name="Status" type="String">  
>        <WHENCHANGED field="MyCorp.State">  
>            <COPY from="value" value="">  
>        </WHENCHANGED>  
> </FIELD>  
> ```  
>  <a name="WhenNotChanged"></a> 

##   Define a field value based on a user not modifying a field (WHENNOTCHANGED)  

In the following example, when a user does not change the value of the MyCorp.State field, the MyCorp.StateDate field becomes read-only.  


> [!div class="tabbedCodeSnippets"]
> ```XML
> <FIELD refname="MyCorp.StateDate" name="Date Of Last State Change" type="DateTime">  
> <!-- Make the StateDate field read-only when the State field is not changed -->  
>        <WHENNOTCHANGED field="MyCorp.State">  
>            <READONLY />  
>        </WHENNOTCHANGED>  
> </FIELD>  
> ```  

## Related articles 
-  [Rules and rule evaluation](../../organizations/settings/work/rule-reference.md)   
