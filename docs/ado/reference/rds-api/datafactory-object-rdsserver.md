---
title: DataFactory 对象 (RDSServer) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 189dc8604883d8d91a8bc223c54dd3cb5c14969e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63134354"
---
# <a name="datafactory-object-rdsserver"></a>DataFactory 对象 (RDSServer)
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 此默认服务器端业务对象实现提供到指定的数据源的客户端应用程序的读/写数据访问的方法。  
  
 **提高**对象被设计为接收客户端请求的服务器端自动化对象。 在 Internet 实现中，它驻留在 Web 服务器上，并通过 ADISAPI 组件实例化。 **提高**对象提供读取和写入访问权限指定的数据源，但不包含任何验证或业务规则逻辑。  
  
 如果你使用中均提供的方法**提高**和[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象，远程数据服务使用**rds。DataControl**默认情况下的版本。 默认值假定基本编程方案中，其中**提高**可作为泛型服务器端业务对象。  
  
 如果你想将 Web 应用程序处理特定于任务的服务器端处理，您可以替换**提高**与自定义业务对象。  
  
 您可以创建调用服务器端业务对象**提高**方法，如[查询](../../../ado/reference/rds-api/query-method-rds.md)并[CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md)。 这是如果你想要将功能添加到您的业务对象，但利用现有的远程数据服务技术，很有帮助。  
  
 **DataFactory**对象不是安全的客户端上运行的脚本。  
  
 类 ID**提高**对象是 9381D8F5 0288年 11 D 0 9501 00AA00B911A5。  
  
 本部分包含以下主题。  
  
-   [DataFactory 对象 (RDSServer) 属性、方法和事件](../../../ado/reference/rds-api/datafactory-object-rdsserver-properties-methods-and-events.md)  
  
## <a name="see-also"></a>请参阅  
 [DataFactory 对象、Query 方法和 CreateObject 方法示例 (VBScript)](../../../ado/reference/rds-api/datafactory-object-query-method-and-createobject-method-example-vbscript.md)


