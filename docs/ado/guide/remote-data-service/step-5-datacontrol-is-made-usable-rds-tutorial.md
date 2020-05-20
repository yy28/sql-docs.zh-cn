---
title: 步骤5： DataControl 可供使用（RDS 教程） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], datacontrol made usable
ms.assetid: ed5c4a24-9804-4c85-817e-317652acb9b4
author: rothja
ms.author: jroth
ms.openlocfilehash: 71576df284f3345d1f72b4043e904ae39ab031d4
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764648"
---
# <a name="step-5-datacontrol-is-made-usable-rds-tutorial"></a>步骤 5：DataControl 变为可用（RDS 教程）
返回的**记录集**对象可供使用。 您可以检查、导航或编辑它，就像对待任何其他**记录集**一样。 您可以对**记录集**执行哪些操作取决于您的环境。 Visual Basic 和 Visual C++ 具有可直接或间接使用**记录集**来实现数据控件的可视化控件。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，Windows 操作系统中不再包含 RDS 服务器组件（有关详细信息，请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)）。 在 Windows 的未来版本中将删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 例如，如果在 Microsoft Internet Explorer 中显示网页，则可能希望在视觉对象控件中显示**记录集**对象数据。 网页上的视觉对象控件无法直接访问**记录集**对象。 但是，它们可以通过 RDS 访问**Recordset**对象[。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)。 **RDS。** 当视觉对象的[SourceRecordset](../../../ado/reference/rds-api/recordset-sourcerecordset-properties-rds.md)属性设置为**Recordset**对象时，DataControl 变得可用。  
  
 视觉对象对象的**DATASRC**参数必须设置为**RDS。DataControl**，并将其**DATAFLD**属性设置为**记录集**对象字段（列）。  
  
 在本教程中，设置**SourceRecordset**属性：  
  
```vb
Sub RDSTutorial5()  
   Dim DS as New RDS.DataSpace  
   Dim RS as ADODB.Recordset  
   Dim DC as New RDS.DataControl  
   Dim DF as Object  
   Set DF = DS.CreateObject("RDSServer.DataFactory", "https://yourServer")  
   Set RS = DF.Query ("DSN=Pubs", "SELECT * FROM Authors")  
   DC.SourceRecordset = RS         ' Visual controls can now bind to DC.  
...  
```  
  
## <a name="see-also"></a>另请参阅  
 [步骤6：将更改发送到服务器（RDS 教程）](../../../ado/guide/remote-data-service/step-6-changes-are-sent-to-the-server-rds-tutorial.md)   
 [RDS 教程 (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
