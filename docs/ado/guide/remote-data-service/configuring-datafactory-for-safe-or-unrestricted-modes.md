---
title: "为安全或不受限制的模式配置 DataFactory |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- DataFactory configuration in RDS [ADO]
ms.assetid: 8ff24805-dc7a-42ae-b600-5bad0e3f51b8
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 745f6c7408f72ee1df0c5757007588b76fe334fc
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="configuring-datafactory-for-safe-or-unrestricted-modes"></a>为安全或不受限制的模式配置 DataFactory
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 默认情况下，使用"安全"安装 ADO[提高](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)配置。 RDS 服务器组件的安全模式意味着在以下情况成立：  
  
1.  需要使用 （这由注册表项设置规定） 提高处理程序。  
  
2.  默认处理程序、 msdfmap.handler，处于已注册、 存在于安全处理程序列表中，并标记为默认处理程序。  
  
3.  Msdfmap.ini 文件安装在 Windows 目录中。 在三层模式下使用 RDS 之前，你必须根据需要，配置此文件。  
  
 （可选） 你可以配置不受限制**DataFactory**安装。 **DataFactory**可以使用直接没有自定义处理程序。 用户仍然可以通过修改连接字符串中，使用自定义处理程序，但它不是必需。 有关使用的影响的详细信息**提高**对象，请参阅[保护 RDS 应用程序](../../../ado/guide/remote-data-service/securing-rds-applications.md)。  
  
 提供了注册表文件 handsafe.reg，用于设置安全配置的处理程序注册表项。 若要在安全模式下运行，运行 handsafe.reg。  
  
 在运行 handsafe.reg 之后, 你必须停止并通过在命令提示符窗口中键入以下命令重新启动 World Wide Web 发布服务在 Web 服务器上:"NET 停止 W3SVC"和"NET 启动 W3SVC"。  
  
## <a name="see-also"></a>另请参阅  
 [DataFactory 自定义项](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [RDS 基础知识](../../../ado/guide/remote-data-service/rds-fundamentals.md)




