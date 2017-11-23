---
title: "评估报表 (AccessToSQL) |Microsoft 文档"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Assessment Report dialog box
- Conversion Report dialog box
ms.assetid: ba6f53aa-0049-4c49-8bb8-607a8bfaa737
caps.latest.revision: "14"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 40f8d07490e74a87c4b505277a523e23349543cb
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="assessment-report-accesstosql"></a>评估报表 (AccessToSQL)
评估报表窗口中显示的数据库的对象添加到转换的结果[!INCLUDE[tsql](../../includes/tsql_md.md)]语法，并且还可以帮助您评估的复杂性和成本的迁移项目。  
  
若要创建评估报表，选择对象要转换的源元数据资源管理器，右键单击**数据库**，然后选择**创建报表**。 你还可以显示此报表自动转换架构之后。 但是，报表名称将转换报表。 有关详细信息，请参阅[项目设置 (GUI) （SSMA 常见）](http://msdn.microsoft.com/en-us/cf06baf1-8714-48a3-95dc-781f6ca53693)。  
  
## <a name="options"></a>选项  
**资源管理器窗格**  
包含在评估报表中的对象的层次结构。 展开文件夹以查看单个对象和子组件。 当你单击类别或对象时，该类别或对象的转换统计信息显示在细节窗格中。  
  
**详细信息窗格中**  
显示转换的所选对象的统计信息或错误和警告消息。 例如，如果选择表文件夹，则详细信息窗格中将显示数量的外键、 索引、 主关键字和已转换的表。  
  
**消息窗格**  
显示错误、 警告和信息性消息时创建评估报表生成。 消息按数字进行分组。  
  
若要查看消息详细信息，请单击**错误**，**警告**，或**消息**，然后展开一条消息。 SSMA 将显示具有此错误的对象的列表。 单击要显示对象的所有转换详细信息的对象。  
  
## <a name="see-also"></a>另请参阅  
[用户界面 Reference(Access)](http://msdn.microsoft.com/en-us/af24c303-4a41-449b-9c86-d6558a97e839)  
  
