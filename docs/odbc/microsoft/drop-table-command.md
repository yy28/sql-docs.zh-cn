---
title: DROP TABLE 命令 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- drop table command [ODBC]
ms.assetid: bc50459b-8861-4889-84a9-129ae9065aa8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 779c519f720027aea3a6f6cf2587d3c6e0b59b52
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303418"
---
# <a name="drop-table-command"></a>DROP TABLE 命令
从使用数据源指定的数据库中删除表，并将其从磁盘中删除。  
  
 Visual FoxPro ODBC 驱动程序支持此命令的本机 Visual FoxPro 语言语法。 有关特定于驱动程序的信息，请参阅备注。  
  
## <a name="syntax"></a>语法  
  
```  
  
DROP TABLE TableName | FileName | ?  
```  
  
## <a name="settings"></a>设置  
 *表名称*  
 指定要从使用数据源指定的数据库中删除的表，并从磁盘中删除表。  
  
 *文件名*  
 指定要从磁盘中删除的可用表。  
  
 ?  
 显示"删除"对话框，您可以从中选择一个表，以便从使用数据源指定的数据库中删除，并从磁盘中删除。  
  
## <a name="remarks"></a>备注  
 发出 DROP TABLE 时，还将删除与表关联的所有主索引、默认值和验证规则。 如果数据库具有与要删除的表关联的规则或关系，则 DROP TABLE 还会影响数据库中用数据源指定的其他表。 当从数据库中删除表时，规则和关系不再有效。  
  
## <a name="driver-remarks"></a>驱动程序备注  
 当应用程序将 ODBC SQL 语句 DROP TABLE 发送到数据源时，Visual FoxPro ODBC 驱动程序使用下表中显示的语法将该命令转换为 Visual FoxProDROP TABLE 命令。  
  
|ODBC 语法|数据源|可视化 FoxPro 语法|  
|-----------------|-----------------|--------------------------|  
|DROP TABLE*基表名称*|数据库（.dbc 文件）|删除*表表名称*删除|  
||可用表目录（.dbf 文件）|ERASE *dbf名称*<br /><br /> ERASE *cdx 名称*<br /><br /> ERASE *fpt 名称*|
