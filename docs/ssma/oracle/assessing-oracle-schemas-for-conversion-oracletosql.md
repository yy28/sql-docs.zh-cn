---
title: "Oracle 架构评估转换 (OracleToSQL) |Microsoft 文档"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Analyzing Conversion Problems
ms.assetid: 4de9bcf6-1346-4740-87f9-7f24a8226357
caps.latest.revision: "7"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: 1489e4002532d09c0085c64f3aea139f21aab2c1
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="assessing-oracle-schemas-for-conversion-oracletosql"></a>Oracle 架构评估转换 (OracleToSQL)
在加载对象并将数据迁移到之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，迁移将十分复杂和多少时间应确定将需要迁移。 SSMA 可以创建显示百分比将成功转换的对象的评估报表。 SSMA 还允许你查看的特定问题导致转换失败。  
  
## <a name="creating-assessment-reports"></a>创建评估报表  
SSMA 时它会创建此评估报告，将转换到所选的 Oracle 数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]语法，然后显示结果。  
  
**创建评估报表**  
  
1.  在 Oracle 元数据资源管理器，选择要评估的架构。  
  
2.  若要省略单个对象，清除那些旁边的复选框。  
  
3.  右键单击**架构**，然后选择**创建报表**。  
  
    您也可以通过右键单击对象，然后选择分析单个对象**创建报表**。  
  
    SSMA 将在窗口底部的状态栏中显示进度。 如果输出窗格可见时，你还将看到输出窗格中的消息。  
  
    评估完成后， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant for Oracle： 将出现评估报表窗口。  
  
## <a name="using-assessment-reports"></a>使用评估报表  
评估报表窗口中包含三个窗格：  
  
-   左窗格中包含评估报表中包含的对象层次的结构。 您可以浏览层次结构，并选择对象和要查看转换统计信息和代码的对象的类别。  
  
-   右窗格中的内容取决于选定的左窗格中的项的。  
  
    如果选择了一组对象，此类架构，或右窗格中的类别窗格中选择某个表时，如果包含转换统计信息窗格和对象。 转换统计信息窗格中显示所选对象的转换统计信息。 按类别窗格中的对象转换为显示统计信息对象或对象的类别。  
  
    如果选择函数、 包、 过程、 序列或视图，则右窗格中将包含统计信息、 源代码和目标代码。  
  
    -   顶部区域显示对象的总体统计信息。 你可能必须展开**统计信息**以查看此信息。  
  
    -   源区域显示所选对象的左窗格中的源代码。 突出显示的区域显示有问题的源代码。  
  
    -   目标区域显示转换后的代码。 红色文本显示有问题的代码和错误消息。  
  
-   底部窗格中显示的消息转换，按消息号分组。 你可以单击**错误**，**警告**，或**信息**来查看消息，类别，然后展开一组消息。 单击各个邮件中的左窗格中选择对象并在右窗格中显示详细信息。  
  
## <a name="analyzing-conversion-problems-by-using-the-assessment-report"></a>使用评估报表来分析转换问题  
转换统计信息窗格中显示转换统计信息。 如果任何类别的百分比是小于 100%，您应该确定为什么转换未成功。  
  
**若要查看转换问题**  
  
1.  通过使用前面的过程中的说明创建评估报表。  
  
2.  在左窗格中，展开架构或具有红色错误图标的文件夹。 继续展开项，直到你选择的转换失败的单个项。  
  
3.  在源窗格的顶部，单击**下一步问题**。  
  
    有问题的代码会突出显示，如下是目标导航窗格中的相关的代码。  
  
4.  查看任何错误消息，，然后确定你想要使用导致转换问题的对象执行操作：  
  
    -   更新 SSMA 中的 Oracle 语法。 你可以更新过程、 函数、 触发器、 打包的函数和打包的过程的语法。 若要更新的语法，在 Oracle 元数据资源管理器窗格中选择的对象，请单击**SQL**选项卡上，然后修改的 SQL 代码。 离开项时，系统将提示你保存已更新的语法。 你可以查看对象报告的错误上**报表**选项卡。  
  
    -   在 Oracle 中，你可以修改 Oracle 对象，可以删除或修改有问题的代码。 若要更新的代码载入 SSMA，你将需要更新的元数据。 有关详细信息，请参阅[连接到 Oracle 数据库 &#40; OracleToSQL &#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md)。  
  
    -   你可以从迁移中排除对象。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]元数据资源管理器和 Oracle 元数据资源管理器中，清除项旁边的复选框，在加载到对象之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]从 Oracle 中迁移数据。  
  
## <a name="next-step"></a>下一步  
[转换 Oracle 架构 &#40; OracleToSQL &#41;](../../ssma/oracle/converting-oracle-schemas-oracletosql.md)  
  
## <a name="see-also"></a>另请参阅  
[将 Oracle 数据库迁移到 SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
