---
title: 评估报表 (MySQLToSQL) |Microsoft 文档
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
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
ms.assetid: 5525d989-024c-402d-9e84-faa4721cc5b9
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 1c591815fc1d32405c0cc63f735fee24d03ce17f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="assessment-report-mysqltosql"></a>评估报表 (MySQLToSQL)
评估报表窗口中显示的数据库的对象添加到转换的结果[!INCLUDE[tsql](../../includes/tsql_md.md)]语法，并且还可以帮助您评估的复杂性和成本的迁移项目。  
  
若要访问评估报表中，选择的对象将转换源元数据资源管理器中右键单击**架构**，然后选择**创建报表**。  
  
## <a name="options"></a>选项  
  
|||  
|-|-|  
|**术语**|**“定义”**|  
|**转换统计信息**|显示按语句类型转换统计信息。 此窗格是可见的组对象，如架构时, 或在左窗格中选择而无需代码的对象。|  
|**按类别的对象**|按类别显示对象的数。 此窗格是可见的组对象，如架构时仅, 或左窗格中选择而无需代码的对象。|  
|**统计信息**|显示所选对象的转换统计信息。 仅当具有代码的单个对象选择左窗格中，此窗格才可见。 你可能必须展开**统计信息**，即立即上面**源**窗格中，若要查看此窗格。|  
|**数据源**|显示所选对象的 MySQL 代码并突出显示未转换为代码[!INCLUDE[tsql](../../includes/tsql_md.md)]。 仅当具有代码的单个对象选择左窗格中，此窗格才可见。<br /><br />单击要设置或清除书签的行号。 使用顶部窗格中的按钮的代码中导航。|  
|**Target**|显示所产生的转换[!INCLUDE[tsql](../../includes/tsql_md.md)]所选的对象和未转换的代码的错误消息代码。 仅当具有代码的单个对象选择左窗格中，此窗格才可见。<br /><br />单击要设置或清除书签的行号。 使用顶部窗格中的按钮的代码中导航。|  
|**消息窗格**|显示错误、 警告和创建评估报表时生成的信息性消息。 消息按数字进行分组。 若要查看导致错误的代码，请单击**错误**，**警告**，或**信息**，展开的消息，类别，然后单击一条消息。|  
  
