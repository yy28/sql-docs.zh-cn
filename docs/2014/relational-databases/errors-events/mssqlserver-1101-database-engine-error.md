---
title: MSSQLSERVER_1101 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1101 (Database Engine error)
ms.assetid: d63b67d5-59f5-4f77-904e-5ba67f2dd850
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ce6210f9ab083315fdd99af5c7559a6b98300644
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553942"
---
# <a name="mssqlserver_1101"></a>MSSQLSERVER_1101
    
## <a name="details"></a>详细信息  
  
|Attribute|值|  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|1101|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|NOALLOCPG|  
|消息正文|由于文件组“%.\*ls”中的磁盘空间不足，无法为数据库“%.*ls”分配新页。 请删除文件组中的对象、将其他文件添加到文件组或者为文件组中的现有文件启用自动增长，以便增加必要的空间。|  
  
## <a name="explanation"></a>说明  
 文件组中没有可用的磁盘空间。  
  
## <a name="user-action"></a>用户操作  
 以下操作可能会使空间在文件组中可用。  
  
-   打开 AUTOGROW。  
  
-   向文件组添加更多文件。  
  
-   通过删除文件组中不必要的索引或表来释放磁盘空间。  
  
  
