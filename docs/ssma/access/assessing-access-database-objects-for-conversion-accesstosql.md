---
title: 用于转换 (AccessToSQL) 评估访问数据库对象 |Microsoft 文档
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- assessing SQL
- assessing syntax
- assessment reports
- creating assessment reports
- estimating migration effort
- reports
- SQL, assessing
- syntax, assessing
ms.assetid: 8b9e23d6-da62-437a-8c05-8ad2628b9441
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 4c2f5bc6953ab0e96397ca728391cbe22a73dd50
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67910692"
---
# <a name="assessing-access-database-objects-for-conversion-accesstosql"></a>评估访问数据库对象的转换 (AccessToSQL)
然后加载对象和数据迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，您应该确定多少的迁移将会成功，并且转换可能需要多长时间。 SSMA 可以创建显示已成功将转换为的对象的百分比评估报告[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 语法和时间估计为执行迁移。 SSMA 还允许您查看特定问题导致转换失败。  
  
## <a name="creating-assessment-reports"></a>创建评估报告  
SSMA 时它创建的评估报告，将转换为所选的访问数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 语法，然后显示结果。  
  
**若要创建评估报告**  
  
1.  访问元数据资源管理器中选择或多个您想要评估的数据库。  
  
2.  若要取消单个对象，清除不希望评估对象旁边的复选框。  
  
3.  用鼠标右键单击**数据库**，然后选择**创建报告**。  
  
    您还可以通过右键单击对象，然后选择分析单个对象**创建报告**。  
  
    SSMA 窗口底部的状态栏中显示进度。 如果输出窗格是可见的您也会看到输出窗格中的消息。  
  
评估完成后， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant for Access:评估报告窗口将出现。  
  
## <a name="using-assessment-reports"></a>使用评估报告  
评估报告窗口包含三个窗格： 资源管理器、 详细信息窗格中和消息窗格。  
  
-   资源管理器窗格允许您浏览得到评估的对象。 您可以单击该窗格以单个表、 索引和键向下钻取的项目。  
  
-   详细信息窗格中显示所选对象的转换统计信息。  
  
-   邮件窗格中显示错误、 警告和信息性消息进行转换，和时间估计用于执行迁移和各个错误纠正的步骤。  
  
您应该再次运行评估报告或转换架构之前更正错误。 若要查找的错误，请单击**错误**中的邮件窗格中，按钮，然后展开要查看发生错误的对象的列表的每个错误。 如果单击 [消息] 窗格中的对象时，所有错误和警告该对象将都出现在详细信息窗格中。  
  
## <a name="next-step"></a>下一步  
[转换 Access 数据库对象](converting-access-database-objects-accesstosql.md)  
  
## <a name="see-also"></a>请参阅  
[Access 数据库迁移到 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
