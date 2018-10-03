---
title: 为安全或不受限制模式下配置数据工厂 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory configuration in RDS [ADO]
ms.assetid: 8ff24805-dc7a-42ae-b600-5bad0e3f51b8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 664a44b9594b77cec07fa4ce7b80afcc0b651323
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47675395"
---
# <a name="configuring-datafactory-for-safe-or-unrestricted-modes"></a>配置用于安全或不受限制模式的 DataFactory
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/en-us/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 默认情况下，使用"安全"安装 ADO[提高](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)配置。 RDS 服务器组件的安全模式意味着在以下情况成立：  
  
1.  需要使用 （这强制要求通过注册表项设置） 提高处理程序。  
  
2.  默认处理程序、 msdfmap.handler，已注册、 在安全处理程序列表中，存在并被标记为默认处理程序。  
  
3.  Msdfmap.ini 文件安装在 Windows 目录中。 在三层模式下使用 RDS 之前，必须根据需要，配置此文件。  
  
 （可选） 你可以配置不受限制**DataFactory**安装。 **数据工厂**可以自定义处理程序不直接使用。 用户仍然可以通过修改连接字符串中，使用自定义处理程序，但不需要。 有关详细信息的使用含义**提高**对象，请参阅[保证 RDS 应用程序](../../../ado/guide/remote-data-service/securing-rds-applications.md)。  
  
 提供了注册表文件 handsafe.reg，若要设置的安全配置的处理程序注册表项。 若要在安全模式下运行，运行 handsafe.reg。  
  
 运行 handsafe.reg 之后, 您必须停止并通过在命令提示符窗口中键入以下命令重新启动 Web 服务器上的 World Wide Web 发布服务:"NET 停止 W3SVC"和"NET 启动 W3SVC"。  
  
## <a name="see-also"></a>请参阅  
 [自定义 DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [RDS 基础知识](../../../ado/guide/remote-data-service/rds-fundamentals.md)



