---
title: "DROP TABLE 命令 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- drop table command [ODBC]
ms.assetid: bc50459b-8861-4889-84a9-129ae9065aa8
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f346bc3701df00cdddf5e6af77f500017570bd51
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="drop-table-command"></a>DROP TABLE 命令
从指定与数据源的数据库中删除一个表并将其从磁盘中删除。  
  
 Visual FoxPro ODBC 驱动程序支持本机 Visual FoxPro 语言语法，此命令。 特定于驱动程序的信息，请参阅备注。  
  
## <a name="syntax"></a>语法  
  
```  
  
DROP TABLE TableName | FileName | ?  
```  
  
## <a name="settings"></a>设置  
 *表名*  
 指定要与数据源指定的数据库中删除并从磁盘中删除的表。  
  
 *FileName*  
 指定用于从磁盘中删除的可用表。  
  
 ?  
 显示删除对话框中，你可以从中选择一个表，从指定与数据源的数据库中删除，若要从磁盘中删除。  
  
## <a name="remarks"></a>注释  
 发出 DROP TABLE 后，还会删除所有主索引、 默认值，以及与该表关联的验证规则。 DROP TABLE 还会影响其他表中的数据库指定与数据源，如果这些表具有规则或要删除的表关联的关系。 从数据库中删除表时，将不再有效的规则和关系。  
  
## <a name="driver-remarks"></a>驱动程序备注  
 当你的应用程序将 ODBC SQL 语句 DROP TABLE 发送到数据源时，Visual FoxPro ODBC 驱动程序将使用下表中所示的语法 Visual FoxProDROP TABLE 命令转换为命令。  
  
|ODBC 语法|数据源|Visual FoxPro 语法|  
|-----------------|-----------------|--------------------------|  
|DROP TABLE*基本表名称*|数据库 （.dbc 文件）|删除表*TableName*删除|  
||可用的表 （.dbf 文件） 的目录|擦除*dbfName*<br /><br /> 擦除*cdxName*<br /><br /> 擦除*fptName*|
