---
title: dBASE Indexes | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DBase indexes [ODBC]
- DBase driver [ODBC], indexes
ms.assetid: fdfa56f5-e324-4ec2-9267-fdf95ab99373
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 66dab60f4a9a180d2a8b74ce4d0c8f4d7bf8d242
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63240398"
---
# <a name="dbase-indexes"></a>dBASE 索引
ODBC dBASE 驱动程序自动打开，并更新 dBASE IV 索引文件。 必须使用**选择索引**显示通过 ODBC 数据源管理器将 dBASE III.ndx 文件与 dBASE 文件相关联的对话框。  
  
 以下限制适用于创建 dBASE 索引：  
  
-   所有列名称必须都是有效的。  
  
-   所有列必须都是相同的升序或降序进行排序。  
  
-   任何单个文本列的长度必须小于 100 个字节。  
  
-   如果存在多个列，所有列必须是文本列和列的大小之和必须小于 100 个字节。  
  
-   备注字段不能创建索引。  
  
-   索引不能指定为当前的字段集 （即，不允许重复的索引）。  
  
-   索引名称必须与匹配 dBASE 索引命名约定。 dBASE III 要求每个索引必须在单独的文件，每个都有.ndx 扩展。 DBASE IV，在索引创建为单个.mdx 文件中存储的标记名称。 .Mdx 文件与数据库文件具有相同的基名称 （例如，Emp.mdx 是 Emp.dbf 数据库的索引文件）。  
  
-   dBASE 定义为从具有相同键值的一组只有一条记录添加到索引中的其中一个唯一索引。
