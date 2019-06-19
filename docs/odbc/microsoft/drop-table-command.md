---
title: DROP TABLE 命令 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0865502928e98329764ae6085ab2b67aa26f0517
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63128029"
---
# <a name="drop-table-command"></a>DROP TABLE 命令
指定与数据源的数据库中移除一个表并从磁盘中删除它。  
  
 Visual FoxPro ODBC 驱动程序支持本机 Visual FoxPro 语言语法，此命令。 特定于驱动程序的信息，请参阅备注。  
  
## <a name="syntax"></a>语法  
  
```  
  
DROP TABLE TableName | FileName | ?  
```  
  
## <a name="settings"></a>设置  
 *TableName*  
 指定从指定的数据源的数据库中删除并从磁盘中删除的表。  
  
 *FileName*  
 指定要从磁盘中删除的可用表。  
  
 ?  
 显示删除对话框中，您可以从中选择一个表，从指定的数据源的数据库中删除，若要从磁盘中删除。  
  
## <a name="remarks"></a>备注  
 当发出 DROP TABLE 时，也会删除所有主索引，默认值，以及与该表关联的验证规则。 DROP TABLE 还会影响其他表中的数据库指定与数据源，如果这些表具有规则或与所要删除的表相关联的关系。 当从数据库中删除表时，都不再有效的规则和关系。  
  
## <a name="driver-remarks"></a>驱动程序备注  
 当你的应用程序将发送到数据源的 ODBC SQL 语句删除表时，Visual FoxPro ODBC 驱动程序将使用下表中所示的语法的 Visual FoxProDROP TABLE 命令转换为该命令。  
  
|ODBC 语法|数据源|Visual FoxPro 语法|  
|-----------------|-----------------|--------------------------|  
|DROP TABLE*基础表名称*|数据库 （.dbc 文件）|删除表*TableName*删除|  
||可用表 （.dbf 文件） 的目录|ERASE *dbfName*<br /><br /> ERASE *cdxName*<br /><br /> ERASE *fptName*|
