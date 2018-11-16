---
title: 步骤 1： 指定服务器程序 （RDS 教程） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], specifying server program
ms.assetid: d8bb35b1-c02a-4231-8d55-016e56e53b95
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5583f9b2c5093859e9bb5d3fd0eb9444828cb4bc
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/12/2018
ms.locfileid: "51558294"
---
# <a name="step-1-specify-a-server-program-rds-tutorial"></a>步骤 1：指定服务器程序（RDS 教程）
在最一般情况下，使用[rds。DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)对象[CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md)方法，以指定默认的服务器程序，[提高](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)，或您自己的自定义服务器程序 （业务对象）。 在服务器和服务器程序的引用实例化服务器程序或*代理*，则返回。  
  
 本教程使用的默认服务器程序：  
  
```vb
Sub RDSTutorial1()  
   Dim DS as New RDS.DataSpace  
   Dim DF as Object  
   Set DF = DS.("RDSServer.DataFactory", "https://yourServer")  
...  
```  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="see-also"></a>请参阅  
 [步骤 2： 调用服务器程序 （RDS 教程）](../../../ado/guide/remote-data-service/step-2-invoke-the-server-program-rds-tutorial.md)   
 [RDS 教程 (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
