---
title: "实现外部元数据 |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-custom-objects
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- disconnected validation [Integration Services]
- connected validation [Integration Services]
- custom data flow components [Integration Services], validating
- validation [Integration Services], components
- metadata [Integration Services]
- data flow components [Integration Services], validating
- data flow components [Integration Services], external metadata
- custom data flow components [Integration Services], external metadata
- external metadata [Integration Services]
ms.assetid: 8f5bd3ed-3e79-43a4-b6c1-435e4c2cc8cc
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 96d413bca20ec171d515ac6d0ad81b5b994bd854
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="implementing-external-metadata"></a>实现外部元数据
  组件与其数据源断开连接后，可以使用 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumnCollection100> 接口，针对组件的外部数据源中的列验证输入和输出列集合中的列。 使用此接口可以保留一份外部数据源中的列的快照，并可以将这些列映射到组件的输入和输出列集合中的列。  
  
 实现外部元数据列会增加组件开发的开销和复杂度，因为您必须额外保留和验证列集合，但这却能节省往返于服务器进行验证的昂贵开销，从而使得这项开发工作是值得的。  
  
## <a name="populating-external-metadata-columns"></a>填充外部元数据列  
 通常，外部元数据列在创建相应的输入或输出列时即添加到集合中。 新列是通过调用 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumnCollection100.New%2A> 方法创建的。 然后，设置列的属性，使其与外部数据源相匹配。  
  
 通过向输入或输出列的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.ExternalMetadataColumnID%2A> 属性分配外部元数据列的 ID，外部元数据列即可映射到相应的输入或输出列。 这使您可以使用集合的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumnCollection100.GetObjectByID%2A> 方法，轻松地查找与特定输入或输出列对应的外部元数据列。  
  
 下面的示例演示如何创建一个外部元数据列，然后通过设置 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.ExternalMetadataColumnID%2A> 属性将其映射到一个输出列。  
  
```csharp  
public void CreateExternalMetaDataColumn(IDTSOutput100 output, int outputColumnID )  
{  
    IDTSOutputColumn100 oColumn = output.OutputColumnCollection.GetObjectByID(outputColumnID);  
    IDTSExternalMetadataColumn100 eColumn = output.ExternalMetadataColumnCollection.New();  
  
    eColumn.DataType = oColumn.DataType;  
    eColumn.Precision = oColumn.Precision;  
    eColumn.Scale = oColumn.Scale;  
    eColumn.Length = oColumn.Length;  
    eColumn.CodePage = oColumn.CodePage;  
  
    oColumn.ExternalMetadataColumnID = eColumn.ID;  
}  
```  
  
```vb  
Public Sub CreateExternalMetaDataColumn(ByVal output As IDTSOutput100, ByVal outputColumnID As Integer)   
 Dim oColumn As IDTSOutputColumn100 = output.OutputColumnCollection.GetObjectByID(outputColumnID)   
 Dim eColumn As IDTSExternalMetadataColumn100 = output.ExternalMetadataColumnCollection.New   
 eColumn.DataType = oColumn.DataType   
 eColumn.Precision = oColumn.Precision   
 eColumn.Scale = oColumn.Scale   
 eColumn.Length = oColumn.Length   
 eColumn.CodePage = oColumn.CodePage   
 oColumn.ExternalMetadataColumnID = eColumn.ID   
End Sub  
```  
  
## <a name="validating-with-external-metadata-columns"></a>使用外部元数据列进行验证  
 对于保留外部元数据列集合的组件，验证还需要完成其他步骤，因为必须验证附加的列集合。 验证可分为连接下的验证和断开连接下的验证。  
  
### <a name="connected-validation"></a>连接下的验证  
 组件与外部数据源处于连接状态时，输入或输出集合中的列是直接与外部数据源相验证的。 另外，还必须验证外部元数据集合中的列。 这是必需的因为可以使用修改外部元数据集合**高级编辑器**中[!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]，并对集合所做的更改不能检测到。 因此，处于连接状态时，组件必须确保外部元数据列集合中的列始终反映外部数据源中的列。  
  
 你可以选择隐藏中的外部元数据集合**高级编辑器**通过设置<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumnCollection100.IsUsed%2A>属性集合的**false**。 但是这还会隐藏**列映射**的编辑器中，它可使用户映射到外部元数据列集合中的列的输入或输出集合中的列的选项卡。 此属性设置为**false**不会阻止开发人员以编程方式修改该集合，但它提供一种外部元数据列集合的一个组件，在以独占方式使用的保护级别[!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]。  
  
### <a name="disconnected-validation"></a>断开连接下的验证  
 组件与外部数据源断开连接后，验证即可简化，因为输入或输出集合中的列将直接与外部元数据集合中的列相验证，而不会验证外部源。 组件应执行断开连接的验证，当未建立到其外部数据源的连接，或者当<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ValidateExternalMetadata%2A>属性是**false**。  
  
 下面的代码示例演示了执行与其外部元数据列集合相验证的组件的实现。  
  
```csharp  
public override DTSValidationStatus Validate()  
{  
    if( this.isConnected && ComponentMetaData.ValidateExternalMetaData )  
    {  
        // TODO: Perform connected validation.  
    }  
    else  
    {  
        // TODO: Perform disconnected validation.  
    }  
}  
```  
  
```vb  
Public  Overrides Function Validate() As DTSValidationStatus   
 If Me.isConnected AndAlso ComponentMetaData.ValidateExternalMetaData Then   
  ' TODO: Perform connected validation.  
 Else   
  ' TODO: Perform disconnected validation.  
 End If   
End Function  
```  

## <a name="see-also"></a>另請參閱  
 [数据流](../../../integration-services/data-flow/data-flow.md)  
  
  

