---
title: MSSQLSERVER_1105 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1105 (Database Engine error)
ms.assetid: e7f4ad02-8c7f-4bb9-9781-2c86253f2138
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e8c01b2e4b9f8621a799756fc4f629d896d85d46
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553932"
---
# <a name="mssqlserver_1105"></a>MSSQLSERVER_1105
    
## <a name="details"></a>详细信息  
  
|Attribute|值|  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|1105|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|NO_MORE_SPACE_IN_FG|  
|消息正文|无法为数据库 '%.\*ls' 中的对象 '%.*ls'%.\*ls 分配空间，因为 '%.\*ls' 文件组已满。 请删除不需要的文件、删除文件组中的对象、将其他文件添加到文件组或为文件组中的现有文件启用自动增长，以便增加可用磁盘空间。|  
  
## <a name="explanation"></a>说明  
 文件组中没有可用的磁盘空间。  
  
## <a name="user-action"></a>用户操作  
 以下操作可能会使空间在文件组中可用：  
  
-   打开 autogrow。  
  
-   向文件组添加更多文件。  
  
-   通过删除不再需要的索引或表来释放磁盘空间。  
  
-   有关详细信息，请参阅 SQL Server 联机丛书中的“解决数据磁盘空间不足的问题”。  
  
> [!NOTE]  
>  当一个索引位于多个文件上时，`ALTER INDEX REORGANIZE` 会在其中一个文件已满后返回错误 1105。 重组进程在尝试将行移到已满的文件时被阻止。 若要消除此限制，执行 `ALTER INDEX REBUILD`，而不是 `ALTER INDEX REORGANIZE`，或提高任何已满文件的文件增长限制。  
  
  
