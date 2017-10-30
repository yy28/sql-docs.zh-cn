---
title: "步骤 5: DataControl 可进行 （RDS 教程） |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- RDS tutorial [ADO], datacontrol made usable
ms.assetid: ed5c4a24-9804-4c85-817e-317652acb9b4
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8f59e167dfad5ddd4b99d784b34e37556a076a2f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="step-5-datacontrol-is-made-usable-rds-tutorial"></a>步骤 5: DataControl 可进行 （RDS 教程）
返回**记录集**对象是可供使用。 你可以检查、 导航，或对其进行编辑，就像任何其他**记录集**。 如何使用**记录集**取决于你的环境。 Visual Basic 和 Visual c + + 提供了可视控件，可以使用**记录集**直接或间接启用的数据控件的帮助。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 例如，如果在 Microsoft Internet Explorer 中显示网页，你可能想要显示**记录集**对象 visual 控件中的数据。 在网页上的可视化控件不能访问**记录集**直接对象。 但是，它们可以访问**记录集**对象通过[rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)。 **Rds.DataControl**可用视觉对象控制其[SourceRecordset](../../../ado/reference/rds-api/recordset-sourcerecordset-properties-rds.md)属性设置为**记录集**对象。  
  
 可视控件对象必须具有其**DATASRC**参数设置为**rds.DataControl**，并将其**DATAFLD**属性设置为**记录集**对象字段 （列）。  
  
 在本教程中，设置**SourceRecordset**属性：  
  
```  
Sub RDSTutorial5()  
   Dim DS as New RDS.DataSpace  
   Dim RS as ADODB.Recordset  
   Dim DC as New RDS.DataControl  
   Dim DF as Object  
   Set DF = DS.CreateObject("RDSServer.DataFactory", "http://yourServer")  
   Set RS = DF.Query ("DSN=Pubs", "SELECT * FROM Authors")  
   DC.SourceRecordset = RS         ' Visual controls can now bind to DC.  
...  
```  
  
## <a name="see-also"></a>另请参阅  
 [步骤 6： 将更改发送到服务器 （RDS 教程）](../../../ado/guide/remote-data-service/step-6-changes-are-sent-to-the-server-rds-tutorial.md)   
 [RDS 教程 (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   

