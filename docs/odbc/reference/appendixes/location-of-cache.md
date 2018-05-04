---
title: 缓存的位置 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: 240d6162-4da6-4b1f-96c7-f379f4ecb16f
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 78e4378e5895e68e8eeb461560faa88ef9cef837
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="location-of-cache"></a>缓存的位置
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 游标库缓存在内存和 Windows® 临时文件中的数据。 此限制仅由可用磁盘空间的是光标库可以处理的结果集的大小。 要缓存的数据将跨段边界，如果插入光标库缓存末尾时使用的临时文件。 但是，要缓存的数据添加 in place of 上次保存的缓存中的数据块。 上次保存的数据块保存在临时文件。 如果游标库终止异常，如当在电源发生故障，它可能会导致 Windows 磁盘上的临时文件。 这些命名 ~ CTT*nnnn*.tmp 和是否在当前目录中创建。  
  
> [!NOTE]  
>  如果从只读共享或光盘 （如 Microsoft 基础类库示例），运行应用程序时，游标库中 Microsoft® WindowsNT®/windows2000 本机尝试在当前目录上的临时文件中缓存数据 SQLSTATEHY000 （常规错误-无法创建文件缓冲区） 将返回。
