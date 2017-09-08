---
title: "评估报表 (SybaseToSQL) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: af24f2c4-5e86-4135-a4f3-a24faaeeefe7
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 1a7de1095387d52d2d7675f1d8b04cc739121636
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="assessment-report-sybasetosql"></a>评估报表 (SybaseToSQL)
评估报表窗口中显示的数据库的对象添加到转换的结果[!INCLUDE[tsql](../../includes/tsql_md.md)]语法，并且还可以帮助您评估的复杂性和成本的迁移项目。  
  
若要访问评估报表中，选择的对象将转换源元数据资源管理器中右键单击**数据库**，然后选择**创建报表**。  
  
## <a name="options"></a>选项  
**转换统计信息**  
显示按语句类型转换统计信息。 此窗格是可见的组对象，如架构时仅, 或左窗格中选择而无需代码的对象。  
  
**按类别列出的对象**  
显示按对象类型转换统计信息。 此窗格是可见的组对象，如架构时仅, 或左窗格中选择而无需代码的对象。  
  
**统计信息**  
显示所选对象的转换统计信息。 仅当具有代码的单个对象选择左窗格中，此窗格才可见。 你可能必须展开**统计信息**若要查看此窗格。  
  
**源导航**  
显示所选对象的 ASE 代码并突出显示未转换为代码[!INCLUDE[tsql](../../includes/tsql_md.md)]。 仅当具有代码的单个对象选择左窗格中，此窗格才可见。  
  
单击要设置或清除书签的行号。 使用顶部窗格中的按钮的代码中导航。  
  
**目标导航**  
显示所产生的转换[!INCLUDE[tsql](../../includes/tsql_md.md)]所选的对象和未转换的代码的错误消息代码。 仅当具有代码的单个对象选择左窗格中，此窗格才可见。  
  
单击要设置或清除书签的行号。 使用顶部窗格中的按钮的代码中导航。  
  
**消息窗格**  
显示错误、 警告和信息性消息时创建评估报表生成。 消息按数字进行分组。 若要查看导致错误的代码，请单击**错误**，**警告**，或**信息**，展开的消息，类别，然后单击一条消息。  
  

