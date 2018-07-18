---
title: 评估报表 (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Assessment Report dialog box
- Conversion Report dialog box
ms.assetid: ba6f53aa-0049-4c49-8bb8-607a8bfaa737
caps.latest.revision: 14
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 8a268b123663b213f3702dde24eba905e38bf1ac
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2018
ms.locfileid: "38980000"
---
# <a name="assessment-report-accesstosql"></a>评估报表 (AccessToSQL)
评估报告窗口会显示到的数据库对象的转换的结果[!INCLUDE[tsql](../../includes/tsql_md.md)]语法，并且还可以帮助您评估的复杂性和成本在迁移项目。  
  
若要创建评估报告，选择对象要转换在源元数据资源管理器，右键单击**数据库**，然后选择**创建报表**。 您还可以显示此报表会自动将架构转换后。 但是，报表名称将是转换报告。 有关详细信息，请参阅[项目设置 (GUI) （SSMA 常见）](http://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693)。  
  
## <a name="options"></a>“常规”  
**资源管理器窗格**  
包含层次结构中评估报告的对象。 展开文件夹以查看各个对象和子组件。 当您单击类别或对象时，该类别或对象的转换统计信息都显示在细节窗格中。  
  
**详细信息窗格**  
显示转换为所选对象的统计信息或错误和警告消息。 例如，如果选择表文件夹，则详细信息窗格将显示外键、 索引、 主键和已转换的表的数字。  
  
**消息窗格**  
显示错误、 警告和信息性消息时创建评估报告生成。 消息按数字进行分组。  
  
若要查看消息详细信息，请单击**错误**，**警告**，或**消息**，然后展开一条消息。 SSMA 会显示具有此错误的对象的列表。 单击要显示对象的所有转换详细信息的对象。  
  
## <a name="see-also"></a>请参阅  
[用户界面 Reference(Access)](http://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
