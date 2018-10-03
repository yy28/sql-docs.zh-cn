---
title: 缓存的位置 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: 240d6162-4da6-4b1f-96c7-f379f4ecb16f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4b1ffd8c56a6727a892cb518222c961bbb6c794c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47649085"
---
# <a name="location-of-cache"></a>缓存的位置
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 避免在新的开发工作中使用此功能并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 游标库缓存在内存中和 Windows® 临时文件中的数据。 这将限制仅由可用磁盘空间游标库可以处理的结果集的大小。 当要缓存的数据将跨越段边界，如果游标库缓存的末尾插入时使用临时文件。 相反，代替上次保存的数据块的缓存中添加要缓存的数据。 上次保存的数据块的保存在临时文件中。 如果游标库异常，终止如时在电源发生故障，它将保留在磁盘上的 Windows 临时文件。 它们被命名为 ~ CTT*nnnn*.tmp 和是否在当前目录中创建。  
  
> [!NOTE]  
>  如果从只读共享或光盘 （如 Microsoft 基础类库示例），运行该应用程序时，游标库中 Microsoft® WindowsNT®/Windows2000 尝试在当前目录上的临时文件中缓存数据 SQLSTATEHY000 （常规错误-无法创建文件缓冲区） 将返回。
