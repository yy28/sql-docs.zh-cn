---
title: DataSpace 对象 (RDS) |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- DataSpace object [RDS]
ms.assetid: 9194bffa-5bdf-4dff-af86-f7158c23bfa7
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ed1ff8e4f9cff153718fa1ccae78a3565183c707
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="dataspace-object-rds"></a>DataSpace 对象 (RDS)
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 创建客户端代理将位于中间层上的自定义业务对象。  
  
 远程数据服务需要数据对象代理，以便客户端组件可以使用位于中间层业务对象进行通信。 代理促进打包、 解包，和传输 （封送处理） 的应用程序的[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)跨进程或计算机边界的数据。  
  
 远程数据服务使用**rds.DataSpace**对象的[CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md)方法创建业务对象代理。 每当创建中间层业务对象对应的实例时，都会动态创建业务对象代理。 远程数据服务支持以下协议： HTTP、 HTTPS （HTTP 安全套接字）、 DCOM、 和进程内 （客户端组件和驻留在同一台计算机上的业务对象）。  
  
> [!NOTE]
>  RDS 中运作的"无状态"方式时**rds.DataSpace**对象使用 HTTP 或 HTTPS 协议。 也就是说，服务器返回的响应后，将被放弃有关客户端请求的任何内部信息。  
  
> [!NOTE]
>  尽管业务对象似乎存在业务对象代理的生存期内，业务对象实际存在仅之前将响应发送到请求。 发送请求后 （即，调用一个方法是在业务对象上），代理会打开新连接到服务器，服务器会创建业务对象的新实例。 对请求作出响应的业务对象后，服务器会业务对象被销毁，并关闭连接。  
  
> [!NOTE]
>  此行为意味着不能将数据从一个请求传递到另一个使用业务对象属性或变量。 必须采用某种其他机制，如文件或的方法自变量，以保留状态数据。  
  
 类 ID **rds.DataSpace**对象是 BD96C556-65A3-11 D 0 983A 00C04FC29E36。  
  
 **DataSpace**对象是可安全执行脚本。  
  
 本部分包含以下主题。  
  
-   [DataSpace 对象 (RDS) 属性、方法和事件](../../../ado/reference/rds-api/dataspace-object-rds-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [DataSpace 对象和 CreateObject 方法示例 (VBScript)](../../../ado/reference/rds-api/dataspace-object-and-createobject-method-example-vbscript.md)


