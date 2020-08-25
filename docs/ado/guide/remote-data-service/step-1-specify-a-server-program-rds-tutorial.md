---
description: 步骤 1：指定服务器程序（RDS 教程）
title: 步骤1： (RDS 教程) 指定服务器程序 |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 32e01e2dd12dcfb098222ffb7c8da0d9a4527d5d
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2020
ms.locfileid: "88759157"
---
# <a name="step-1-specify-a-server-program-rds-tutorial"></a>步骤 1：指定服务器程序（RDS 教程）
在最常见的情况下，使用 [RDS。空间](../../reference/rds-api/dataspace-object-rds.md) 对象 [CreateObject](../../reference/rds-api/createobject-method-rds.md) 方法，用于指定默认服务器程序、 [RDSServer](../../reference/rds-api/datafactory-object-rdsserver.md)或您自己的自定义服务器程序 (业务对象) 。 服务器程序在服务器上实例化，并返回对服务器程序或 *代理*的引用。  
  
 本教程使用默认服务器程序：  
  
```vb
Sub RDSTutorial1()  
   Dim DS as New RDS.DataSpace  
   Dim DF as Object  
   Set DF = DS.("RDSServer.DataFactory", "https://yourServer")  
...  
```  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，Windows 操作系统中不再包含 RDS 服务器组件 (参阅 Windows 8 和 [Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416) ，以了解更多详细信息) 。 在 Windows 的未来版本中将删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到 [WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="see-also"></a>另请参阅  
 [步骤2：调用服务器程序 (RDS 教程) ](./step-2-invoke-the-server-program-rds-tutorial.md)   
 [RDS 教程 (VBScript)](./rds-tutorial-vbscript.md)