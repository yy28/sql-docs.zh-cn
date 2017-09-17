---
title: "dBASE 索引 |Microsoft 文档"
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
- DBase indexes [ODBC]
- DBase driver [ODBC], indexes
ms.assetid: fdfa56f5-e324-4ec2-9267-fdf95ab99373
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9f2725f312691d3cb644f9a096b5f469f1356c55
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="dbase-indexes"></a>dBASE 索引
ODBC dBASE 驱动程序将自动打开，并更新 dBASE IV 索引文件。 必须使用**选择索引**对话框中显示通过 ODBC 数据源管理器将 dBASE III.ndx 文件相关联的 dBASE 文件。  
  
 以下限制适用于创建 dBASE 索引：  
  
-   所有列名称必须都是有效的。  
  
-   所有列必须都是相同的升序或降序排序。  
  
-   任何单个文本列的长度必须小于 100 个字节。  
  
-   如果存在多个列，所有列必须是文本列和列的大小之和必须小于 100 个字节。  
  
-   无法创建索引备注字段。  
  
-   索引不能指定字段的当前集 （即，不允许重复的索引）。  
  
-   索引名称必须匹配 dBASE 索引命名约定。 dBASE III 要求每个索引必须在单独的文件，每个都有.ndx 扩展。 在 dBASE IV，索引创建为存储在单个.mdx 文件中的标记名称。 .Mdx 文件与数据库文件具有相同的基名称 （例如，Emp.mdx 是 Emp.dbf 数据库的索引文件）。  
  
-   dBASE 定义为从具有相同键值的一组只有一条记录添加到索引的下一个唯一索引。
