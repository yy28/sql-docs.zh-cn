---
description: 在用于 DCOM 的客户端中注册业务对象
title: 在客户端上注册业务对象以与 DCOM 一起使用 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- business objects in RDS [ADO]
ms.assetid: 75a21910-607f-463a-ae18-a17130dafb7e
author: rothja
ms.author: jroth
ms.openlocfilehash: 611ebf58419d893b5295bd2a7370cc9ac71c74b1
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88977788"
---
# <a name="registering-business-objects-on-the-client-for-use-with-dcom"></a>在用于 DCOM 的客户端中注册业务对象
自定义业务对象需要确保客户端可以将其程序名称 (ProgId) 映射到可通过 DCOM 使用的标识符 (CLSID) 。 出于此原因，DCOM 对象的 ProgID 必须位于客户端注册表中，并映射到服务器端业务对象的类 ID。 对于其他支持的协议 (HTTP、HTTPS 和进程内) ，这并不是必需的。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，Windows 操作系统中不再包含 RDS 服务器组件 (参阅 Windows 8 和 [Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416) ，以了解更多详细信息) 。 在 Windows 的未来版本中将删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到 [WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 例如，如果使用特定类 ID 公开名为 MyBObj 的服务器端业务对象（例如 "{00112233-4455-6677-8899-00AABBCCDDEE}"），请确保将以下条目添加到客户端注册表：  
  
```console
[HKEY_CLASSES_ROOT]  
\MyBObj\Clsid\(Default) "{00112233-4455-6677-8899-00AABBCCDDEE}"  
```


