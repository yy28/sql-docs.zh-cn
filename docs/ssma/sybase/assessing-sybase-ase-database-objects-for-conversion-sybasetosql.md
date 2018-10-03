---
title: 评估 SAP ASE 数据库对象的转换 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 12/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: eb996b7c-1eef-4f73-b5e6-2fa6faf7336c
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: e7d1b0b68835fe8b909369a87814a3d1c41e07d1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47841055"
---
# <a name="assessing-sap-ase-database-objects-for-conversion-sybasetosql"></a>评估 SAP ASE 数据库对象的转换 (SybaseToSQL)
在加载对象并将数据迁移到之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL，则应确定如何迁移的复杂度和应该花费多少时间。 SSMA 可以创建显示的对象和过程的成功转换为百分比的评估报告[!INCLUDE[tsql](../../includes/tsql-md.md)]。 SSMA 还允许您查看可能会导致转换失败的特定问题。  
  
## <a name="create-assessment-reports"></a>创建评估报告  
SSMA 创建此评估报表时，将转换为所选的 SAP Adaptive Server Enterprise (ASE) 数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL 语法，然后显示结果。  
  
**若要创建评估报告**  
  
1.  Sybase 元数据资源管理器中选择你想要评估的数据库。  
  
2.  若要省略单个对象，清除你不想要评估的对象旁边的复选框。  
  
3.  用鼠标右键单击**数据库**，然后选择**创建报告**。  
  
    你也可以通过右键单击对象，然后选择分析单个对象**创建报表**。  
  
    SSMA 窗口底部的状态栏中显示进度。 如果输出窗格可见时，还将看到相关的任何消息。  
  
    评估完成后， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant for Sybase： 评估报告窗口中会显示。  
  
## <a name="use-assessment-reports"></a>使用评估报告  
评估报告窗口包含三个窗格：  
  
-   左窗格中包含评估报告中包含的对象的层次的结构。 您可以浏览层次结构，并选择对象和对象类别，若要查看转换统计信息和代码。  
  
-   根据在左窗格中选择哪一项的右窗格中的内容而异。  
  
    如果选择的一组对象 （如架构） 或表，则在右窗格显示两个窗格。 **的转换统计**窗格显示所选对象的转换统计信息。 **按类别对象**窗格显示了对象或类别的对象的转换统计信息。  
  
    如果选择了存储的过程、 视图或触发器，右侧窗格中包含的统计信息、 源代码和目标代码。  
  
    -   顶部区域中显示对象的总体统计信息。 您可能需要展开**统计信息**查看此信息。 
    -   源区域显示了在左窗格中选择的对象的源代码。 突出显示的区域显示有问题的源代码。  
    -   目标区域显示转换后的代码。 红色文本显示了有问题的代码和错误消息。  
  
-   在底部窗格显示了转换消息，按消息编号分组。 选择**错误**，**警告**，或**信息**若要查看的消息，类别，然后展开一组消息。 单击选择的对象，然后显示左的窗格中的单个消息中的右窗格的详细信息。  
  
## <a name="analyze-conversion-problems-by-using-the-assessment-report"></a>使用评估报告分析转换问题  
**的转换统计窗格**显示的转换统计信息。 如果任何类别的百分比低于 100%，应确定为何转换未成功。  
  
**若要查看转换问题**  
  
1.  通过使用前面的过程中的说明创建评估报告。  
  
2.  在左窗格中，展开架构或具有红色错误图标的文件夹。 继续展开项，直至选择失败，转换的单个项。  
  
3.  在源窗格顶部，选择**下一个问题**。  
    有问题的代码会突出显示，是中的相关的代码**目标导航**窗格。  
  
4.  查看任何错误消息，，然后确定你想要使用导致转换问题的对象执行操作：  
  
    -   更新在 SSMA 中的 ASE 语法。 您可以更新仅针对存储的过程和触发器的语法。 若要更新的语法，请在 Sybase 元数据资源管理器窗格中选择的对象，单击**SQL**选项卡，然后单击 SQL 代码。 当你离开该项时，系统会提示保存已更新的语法。 查看报告的错误的对象上**报表**选项卡。  
  
    -   在 ASE 中，您可以更改 ASE 对象以删除或修改有问题的代码。 若要将更新的代码加载到 SSMA，必须更新元数据。 有关详细信息，请参阅[连接到 Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md)。  
  
    -   您可以从迁移中排除对象。 在中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL 元数据资源管理器和 Sybase 元数据资源管理器中，清除项旁边的复选框，然后加载到对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL 和 ASE 中迁移数据。
  
## <a name="next-steps"></a>后续步骤  
[转换 SAP ASE 数据库对象&#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)  
  
## <a name="see-also"></a>请参阅  
[SAP ASE 数据库迁移到 SQL Server-Azure SQL 数据库&#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
