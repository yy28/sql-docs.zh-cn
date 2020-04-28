---
title: DataFactory 对象（RDSServer） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- DataFactory object [ADO]
ms.assetid: e75240c2-b749-471e-b6ea-98cae232efbe
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 97597e15bc5cd8ee8d3008c97f3a4e8b07b2d43d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "67964324"
---
# <a name="datafactory-object-rdsserver"></a>DataFactory 对象 (RDSServer)
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，Windows 操作系统中不再包含 RDS 服务器组件（有关详细信息，请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)）。 在 Windows 的未来版本中将删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 此默认服务器端业务对象实现为客户端应用程序提供对指定数据源的读/写数据访问的方法。  
  
 **RDSServer. DataFactory**对象设计为接收客户端请求的服务器端自动化对象。 在 Internet 实现中，它驻留在 Web 服务器上，由 ADISAPI 组件实例化。 **RDSServer. DataFactory**对象提供对指定数据源的读写访问权限，但不包含任何验证或业务规则逻辑。  
  
 如果使用在**RDSServer. DataFactory**和 RDS 中都可用的方法。 [DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象，远程数据服务使用**RDS。** 默认情况下，DataControl 版本。 默认情况下，使用的是一个基本的编程方案，其中， **RDSServer DataFactory**用作泛型服务器端业务对象。  
  
 如果你希望你的 Web 应用程序处理特定于任务的服务器端处理，则可以使用自定义业务对象替换**RDSServer. DataFactory。**  
  
 你可以创建调用**RDSServer. DataFactory**方法的服务器端业务对象，例如[Query](../../../ado/reference/rds-api/query-method-rds.md)和[CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md)。 如果要将功能添加到业务对象，但要利用现有远程数据服务技术，这会很有帮助。  
  
 对于在客户端运行的脚本， **DataFactory**对象是不安全的。  
  
 **DataFactory**对象的类 ID 是9381D8F5-0288-11D0-9501-00AA00B911A5。  
  
 本部分包含以下主题。  
  
-   [DataFactory 对象 (RDSServer) 属性、方法和事件](../../../ado/reference/rds-api/datafactory-object-rdsserver-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [DataFactory 对象、Query 方法和 CreateObject 方法示例 (VBScript)](../../../ado/reference/rds-api/datafactory-object-query-method-and-createobject-method-example-vbscript.md)


