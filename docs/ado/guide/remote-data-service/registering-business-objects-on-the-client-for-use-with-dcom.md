---
title: 注册 DCOM 使用的客户端上的业务对象 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- business objects in RDS [ADO]
ms.assetid: 75a21910-607f-463a-ae18-a17130dafb7e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4094d147e47bd39298b6dd94b4819eaa3d650eb6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47691005"
---
# <a name="registering-business-objects-on-the-client-for-use-with-dcom"></a>在用于 DCOM 的客户端中注册业务对象
自定义业务对象需要确保客户端可以将其程序名称 (ProgId) 映射到可以通过 DCOM 使用的标识符 (CLSID)。 出于此原因，DCOM 对象的 ProgID 必须为客户端的注册表中，将映射到的服务器端业务对象的类 ID。 对于其他支持的协议 （HTTP、 HTTPS 和进程内），这是不必要。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/en-us/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 例如，如果公开服务器端业务对象 mybobj 特定的类 id，例如，"{00112233-4455-6677-8899-00AABBCCDDEE}"，请确保，将以下条目添加到客户端的注册表：  
  
```  
[HKEY_CLASSES_ROOT]  
\MyBObj\Clsid\(Default) "{00112233-4455-6677-8899-00AABBCCDDEE}"  
```


