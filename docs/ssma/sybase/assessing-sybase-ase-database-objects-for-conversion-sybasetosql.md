---
title: "评估 Sybase ASE 数据库对象的转换 (SybaseToSQL) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: eb996b7c-1eef-4f73-b5e6-2fa6faf7336c
caps.latest.revision: "7"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ae77c759c4856ecb3b74cbaeb36f0123398c2e16
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="assessing-sybase-ase-database-objects-for-conversion-sybasetosql"></a>用于转换 (SybaseToSQL) 的评估 Sybase ASE 数据库对象
在加载对象并将数据迁移到之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，你应该确定迁移将十分复杂和多少时间迁移过程将需要。 SSMA 可以创建显示的对象和将成功转换为的过程的百分比评估报表[!INCLUDE[tsql](../../includes/tsql_md.md)]。 SSMA 还允许你查看将导致转换失败的特定问题。  
  
## <a name="creating-assessment-reports"></a>创建评估报表  
SSMA 时它会创建此评估报告，将转换到所选的 Sybase 自适应 Server Enterprise (ASE) 数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 语法，然后显示结果。  
  
**创建评估报表**  
  
1.  在 Sybase 元数据资源管理器中，选择你想要评估的数据库。  
  
2.  若要省略单个对象，清除你不想要评估的对象旁边的复选框。  
  
3.  右键单击**数据库**，然后选择**创建报表**。  
  
    您也可以通过右键单击对象，然后选择分析单个对象**创建报表**。  
  
    SSMA 将在窗口底部的状态栏中显示进度。 如果输出窗格可见时，你还将看到输出窗格中的消息。  
  
    评估完成后， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Sybase 迁移助手： 将出现评估报表窗口。  
  
## <a name="using-assessment-reports"></a>使用评估报表  
评估报表窗口中包含三个窗格：  
  
-   左窗格中包含评估报表中包含的对象层次的结构。 您可以浏览层次结构和选择对象和类别的对象序列化为查看转换统计信息和代码。  
  
-   右窗格中的内容取决于选定的左窗格中的项。  
  
    如果选择一组对象，则选择此类架构或表右窗格中包含的转换统计信息窗格和对象类别窗格。 转换统计信息窗格中显示所选对象的转换统计信息。 按类别窗格中的对象转换为显示统计信息对象或对象的类别。  
  
    如果选择存储的过程、 视图或触发器，则右窗格中将包含统计信息、 源代码和目标代码。  
  
    -   顶部区域显示对象的总体统计信息。 你可能必须展开**统计信息**以查看此信息。  
  
    -   源区域显示所选对象的左窗格中的源代码。 突出显示的区域显示有问题的源代码。  
  
    -   目标区域显示转换后的代码。 红色文本显示有问题的代码和错误消息。  
  
-   底部窗格中显示的消息转换，按消息号分组。 你可以单击**错误**，**警告**，或**信息**来查看消息，类别，然后展开一组消息。 单击各个邮件中的左窗格中选择对象并在右窗格中显示详细信息。  
  
## <a name="analyzing-conversion-problems-using-the-assessment-report"></a>使用评估报表的分析转换问题  
转换统计信息窗格显示转换统计信息。 如果任何类别的百分比是小于 100%，您应该确定为什么转换未成功。  
  
**若要查看转换问题**  
  
1.  通过使用前面的过程中的说明创建评估报表。  
  
2.  在左窗格中，展开架构或具有红色错误图标的文件夹。 继续展开项，直到你选择的转换失败的单个项。  
  
3.  在源窗格的顶部，单击**下一步问题**。  
  
    有问题的代码会突出显示，如下是目标导航窗格中的相关的代码。  
  
4.  查看任何错误消息，，然后确定你想要使用导致转换问题的对象执行操作：  
  
    -   更新中 SSMA 的 ASE 语法。 你可以更新仅适用于存储的过程和触发器的语法。 若要更新的语法，在 Sybase 元数据资源管理器窗格中选择的对象，请单击**SQL**选项卡上，然后编辑的 SQL 代码。 离开项时，系统将提示你保存已更新的语法。 你可以查看对象报告的错误上**报表**选项卡。  
  
    -   在 ASE 中，你可能会改变 ASE 对象，可以删除或修改有问题的代码。 若要更新的代码载入 SSMA，你将需要更新的元数据。 有关详细信息，请参阅[连接到 Sybase ASE &#40;SybaseToSQL &#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md).  
  
    -   你可以从迁移中排除对象。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 元数据资源管理器和 Sybase 元数据资源管理器中，清除项旁边的复选框，在加载到对象之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 和 ASE 中迁移数据。  
  
## <a name="next-step"></a>下一步  
[转换 Sybase ASE 数据库对象 &#40;SybaseToSQL &#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)  
  
## <a name="see-also"></a>另请参阅  
[Sybase ASE 将数据库迁移到 SQL Server 的 Azure SQL DB &#40;SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
