---
description: dBASE 索引
title: dBASE 索引 |Microsoft Docs
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
ms.openlocfilehash: 30a6390f0e187cc063b2a650af2da3b9fcc87d57
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340953"
---
# <a name="dbase-indexes"></a>dBASE 索引
ODBC dBASE 驱动程序会自动打开并更新 dBASE IV 索引文件。 必须使用通过 ODBC 数据源管理器显示的 " **选择索引** " 对话框，将 dbase ndx 文件与 dbase 文件相关联。  
  
 以下限制适用于创建 dBASE 索引：  
  
-   所有列名称必须有效。  
  
-   所有列都必须采用相同的升序或降序顺序。  
  
-   任何单个文本列的长度必须小于100个字节。  
  
-   如果存在多个列，则所有列必须是文本列，列大小之和必须小于100个字节。  
  
-   无法为备注字段编制索引。  
  
-   不得为当前字段集指定索引 (也就是说，不允许) 重复的索引。  
  
-   索引名称必须与 dBASE 索引命名约定匹配。 dBASE III 要求每个索引位于单独的文件中，每个索引都具有扩展名 ndx。 在 dBASE IV 中，索引创建为存储在单个 mdx 文件中的标记名称。 该 mdx 文件与数据库文件具有相同的基名称 (例如，Emp 是 Emp 数据库) 的索引文件。  
  
-   dBASE 定义唯一索引，其中只有一个具有相同键值的集中的记录添加到索引中。
