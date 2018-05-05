---
title: 评估访问数据库对象的转换 (AccessToSQL) |Microsoft 文档
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-access
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
- assessing SQL
- assessing syntax
- assessment reports
- creating assessment reports
- estimating migration effort
- reports
- SQL, assessing
- syntax, assessing
ms.assetid: 8b9e23d6-da62-437a-8c05-8ad2628b9441
caps.latest.revision: 16
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: fb353f5906c1ed5cb45d6075f92cf183ba5e276b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="assessing-access-database-objects-for-conversion-accesstosql"></a>评估转换 (AccessToSQL) 访问数据库对象
在加载对象并将数据迁移到之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，你应确定多少的迁移将会成功，并转换可能需要多长时间。 SSMA 可以创建显示已成功将转换为对象的百分比评估报表[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 语法和时间估计执行的迁移。 SSMA 还允许你查看特定的问题导致转换失败。  
  
## <a name="creating-assessment-reports"></a>创建评估报表  
SSMA 当它创建评估报表时，将转换到所选的访问数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 语法，然后显示结果。  
  
**创建评估报表**  
  
1.  在访问元数据资源管理器，选择你想要评估的数据库。  
  
2.  若要省略单个对象，清除你不想要评估对象旁边的复选框。  
  
3.  右键单击**数据库**，然后选择**创建报表**。  
  
    您也可以通过右键单击一个对象，然后选择分析单个对象**创建报表**。  
  
    SSMA 在窗口底部的状态栏中显示进度。 如果输出窗格可见时，你还将看到输出窗格中的消息。  
  
评估完成后， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant for Access： 出现评估报表窗口。  
  
## <a name="using-assessment-reports"></a>使用评估报表  
评估报表窗口包含三个窗格： 资源管理器、 的详细信息窗格中，和消息窗格。  
  
-   资源管理器窗格中，可以浏览中接受评估的对象。 你可以单击此窗格可以深化到各个表、 索引和密钥中的项。  
  
-   详细信息窗格显示所选对象的转换统计信息。  
  
-   消息窗格中显示错误、 警告和信息性消息进行转换，和时间的估计值用于执行的迁移和各个错误更正步骤。  
  
你应更正错误，然后再次运行评估报表或转换架构。 若要找到错误，请单击**错误**中消息窗格中，按钮，然后展开每个错误，若要查看的对象发生错误的列表。 如果单击消息窗格中的某个对象时，所有错误和警告为该对象将都显示在细节窗格中。  
  
## <a name="next-step"></a>下一步  
[转换 Access 数据库对象](http://msdn.microsoft.com/en-us/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)  
  
## <a name="see-also"></a>另请参阅  
[将访问数据库迁移到 SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
