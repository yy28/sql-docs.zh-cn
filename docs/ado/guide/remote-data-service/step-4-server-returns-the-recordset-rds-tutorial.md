---
title: 步骤 4： 服务器返回记录集 （RDS 教程） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], server returns Recordset
ms.assetid: 3d1855c4-419c-4810-b5ea-6c874b5e2905
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f111fab97b81ed847870f6535399c58bd856ab99
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/12/2018
ms.locfileid: "51559654"
---
# <a name="step-4-server-returns-the-recordset-rds-tutorial"></a>步骤 4：服务器返回记录集（RDS 教程）
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 将检索到 RDS**记录集**向窗体可以发送回客户端对象 (也就是说，它*封送***记录集**)。 转换和如何发送的确切形式取决于是否在服务器位于 Internet 或 intranet，本地网络，或者是一个动态链接库。 但是，此详细信息并不重要;将发送所有相关问题是该 RDS**记录集**返回给客户端。  
  
 客户端侧**记录集**返回对象并将其分配给本地变量。  
  
```vb
Sub RDSTutorial4()  
   Dim DS as New RDS.DataSpace  
   Dim RS as ADODB.Recordset  
   Dim DF as Object  
   Set DF = DS.CreateObject("RDSServer.DataFactory", "https://yourServer")  
   Set RS = DF.Query("DSN=Pubs", "SELECT * FROM Authors")  
...  
```  
  
## <a name="see-also"></a>请参阅  
 [步骤 5: DataControl 是变为可用选 （RDS 教程）](../../../ado/guide/remote-data-service/step-5-datacontrol-is-made-usable-rds-tutorial.md)   
 [RDS 教程 (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
