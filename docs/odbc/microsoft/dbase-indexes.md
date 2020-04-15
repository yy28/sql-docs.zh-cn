---
title: dBASE 指数 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9300a38a0e36da771a238f73b77d3dda527334ae
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307668"
---
# <a name="dbase-indexes"></a>dBASE 索引
ODBC dBASE 驱动程序自动打开并更新 dBASE IV 索引文件。 您必须使用通过 ODBC 数据源管理员显示**的"选择索引"** 对话框将 dBASE III .ndx 文件与 dBASE 文件相关联。  
  
 以下限制适用于 dBASE 索引的创建：  
  
-   所有列名称必须有效。  
  
-   所有列必须以相同的升序或降序排列。  
  
-   任何单个文本列的长度必须小于 100 字节。  
  
-   如果存在多个列，则所有列都必须为文本列，并且列大小的总和必须小于 100 字节。  
  
-   无法对备忘录字段进行索引。  
  
-   不得为当前字段集指定索引（即不允许重复索引）。  
  
-   索引名称必须与 dBASE 索引命名约定匹配。 dBASE III 要求每个索引位于一个单独的文件中，每个索引都有一个 .ndx 扩展名。 在 dBASE IV 中，索引创建为存储在单个 .mdx 文件中的标记名称。 .mdx 文件与数据库文件具有相同的基本名称（例如，Emp.mdx 是 Emp.dbf 数据库的索引文件）。  
  
-   dBASE 将唯一索引定义为在索引中仅将具有相同键值集中的一条记录添加到索引中。
