---
title: DataSpace 对象 (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- DataSpace object [RDS]
ms.assetid: 9194bffa-5bdf-4dff-af86-f7158c23bfa7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 078799f90a0241dc29f30693adce95ea2e795ff8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47654265"
---
# <a name="dataspace-object-rds"></a>DataSpace 对象 (RDS)
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/en-us/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 创建自定义业务对象位于中间层上的客户端代理。  
  
 远程数据服务需要业务对象代理，以便客户端组件可以与位于中间层业务对象进行通信。 代理方便打包、 解包，和传输 （封送处理） 的应用程序的[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)跨进程或计算机边界的数据。  
  
 远程数据服务使用**rds。DataSpace**对象的[CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md)方法来创建业务对象代理。 每当创建的中间层业务对象对应的实例时，都会动态创建的业务对象代理。 远程数据服务支持以下协议： HTTP、 HTTPS （HTTP 安全套接字）、 DCOM 和进程内 （客户端组件和业务对象驻留在同一台计算机上）。  
  
> [!NOTE]
>  RDS 的行为"无状态"方式时**rds。数据空间**对象使用的 HTTP 或 HTTPS 协议。 也就是说，服务器返回响应后，将被放弃有关客户端请求的任何内部信息。  
  
> [!NOTE]
>  尽管业务对象似乎存在业务对象代理的生存期内，业务对象实际存在仅之前的请求发送响应。 发送请求后 （即，调用某个方法时对业务对象），代理会打开新的连接到服务器，服务器会创建业务对象的新实例。 业务对象响应请求后，服务器会破坏业务对象，并关闭连接。  
  
> [!NOTE]
>  此行为意味着不能将数据从一个请求传递到另一个使用业务对象属性或变量。 必须采用某种其他机制，如文件或方法参数时，将状态数据持久保存。  
  
 类 ID **rds。数据空间**对象是 BD96C556-65A3-11 D 0 983A 00C04FC29E36。  
  
 **DataSpace**对象是可安全执行脚本。  
  
 本部分包含以下主题。  
  
-   [DataSpace 对象 (RDS) 属性、方法和事件](../../../ado/reference/rds-api/dataspace-object-rds-properties-methods-and-events.md)  
  
## <a name="see-also"></a>请参阅  
 [DataSpace 对象和 CreateObject 方法示例 (VBScript)](../../../ado/reference/rds-api/dataspace-object-and-createobject-method-example-vbscript.md)


