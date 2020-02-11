---
title: 空间对象（RDS） |Microsoft Docs
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
ms.openlocfilehash: bbd27490e20e8c615ba934299e80f55eb06a5481
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67964359"
---
# <a name="dataspace-object-rds"></a>DataSpace 对象 (RDS)
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，Windows 操作系统中不再包含 RDS 服务器组件（有关详细信息，请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)）。 在 Windows 的未来版本中将删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 创建位于中间层上的自定义业务对象的客户端代理。  
  
 远程数据服务需要业务对象代理，以便客户端组件可以与位于中间层的业务对象通信。 代理有助于跨进程或计算机边界对应用程序的[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)数据进行打包、unpackaging 和传输（封送处理）。  
  
 远程数据服务使用**RDS。** 用于创建业务对象代理的空间对象的[CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md)方法。 每次创建业务对象代理中间层业务对象对应项的实例时，都会动态创建该代理。 远程数据服务支持以下协议： HTTP、HTTPS （HTTP 安全套接字）、DCOM 和进程内（客户端组件和业务对象驻留在同一台计算机上）。  
  
> [!NOTE]
>  Rds 时，RDS 的行为方式为 "无状态" **。空间**对象使用 HTTP 或 HTTPS 协议。 也就是说，在服务器返回响应后，任何有关客户端请求的内部信息都将被丢弃。  
  
> [!NOTE]
>  尽管业务对象在业务对象代理的生存期内似乎存在，但只有在将响应发送到请求之后，业务对象才会实际存在。 发出请求时（即，在业务对象上调用方法），代理将打开到服务器的新连接，并且服务器会创建业务对象的新实例。 业务对象响应请求后，服务器会销毁业务对象并关闭连接。  
  
> [!NOTE]
>  此行为意味着不能使用业务对象属性或变量将数据从一个请求传递到另一个请求。 必须使用某种其他机制（如文件或方法参数）来持久保存状态数据。  
  
 RDS 的类 ID **。空间**对象为 BD96C556-65A3-11D0-983A-00C04FC29E36。  
  
 对于脚本编写，"**空间**" 对象是安全的。  
  
 本部分包含以下主题。  
  
-   [DataSpace 对象 (RDS) 属性、方法和事件](../../../ado/reference/rds-api/dataspace-object-rds-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [DataSpace 对象和 CreateObject 方法示例 (VBScript)](../../../ado/reference/rds-api/dataspace-object-and-createobject-method-example-vbscript.md)


