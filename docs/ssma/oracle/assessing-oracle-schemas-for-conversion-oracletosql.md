---
title: 评估 Oracle 架构以进行转换 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Analyzing Conversion Problems
ms.assetid: 4de9bcf6-1346-4740-87f9-7f24a8226357
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 0ff56be1b7da0376250c7ed021ae78d7144a7645
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264552"
---
# <a name="assessing-oracle-schemas-for-conversion-oracletosql"></a>评估 Oracle 架构以进行转换 (OracleToSQL)
在加载对象并将数据迁移到之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，应确定迁移将复杂程度，并且多长时间的迁移。 SSMA 可以创建评估报告，显示将成功转换的对象的百分比。 SSMA 还可以查看特定问题，导致转换失败。  
  
## <a name="creating-assessment-reports"></a>创建评估报告  
SSMA 时创建此评估报表时，将转换为所选的 Oracle 数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]语法，然后显示结果。  
  
**若要创建评估报告**  
  
1.  在 Oracle 元数据资源管理器，选择要评估的架构。  
  
2.  若要省略单个对象，清除那些旁边的复选框。  
  
3.  右键单击**架构**，然后选择**创建报表**。  
  
    你也可以通过右键单击对象，然后选择分析单个对象**创建报表**。  
  
    SSMA 会在窗口底部的状态栏中显示进度。 如果输出窗格是可见的您也会看到输出窗格中的消息。  
  
    评估完成后， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant for Oracle:将出现评估报表窗口。  
  
## <a name="using-assessment-reports"></a>使用评估报告  
评估报告窗口包含三个窗格：  
  
-   左窗格中包含评估报告中包含的对象的层次的结构。 您可以浏览层次结构，并选择对象和类别的对象，若要查看转换统计信息和代码。  
  
-   在右窗格的内容取决于在左窗格中选择的项。  
  
    如果选择的一组对象，则此类架构，或右窗格中的类别窗格如果选定一个表，包含转换的统计信息窗格和对象。 转换的统计信息窗格中显示所选对象的转换统计信息。 对象的类别窗格显示了对象或类别的对象的转换统计信息。  
  
    如果选择了函数、 包、 过程、 序列或视图，右侧窗格中包含的统计信息、 源代码和目标代码。  
  
    -   顶部区域中显示对象的总体统计信息。 您可能需要展开**统计信息**查看此信息。  
  
    -   源区域显示了在左窗格中选择的对象的源代码。 突出显示的区域显示有问题的源代码。  
  
    -   目标区域显示转换后的代码。 红色文本显示了有问题的代码和错误消息。  
  
-   在底部窗格显示了转换消息，按消息编号分组。 可以单击**错误**，**警告**，或**信息**若要查看的消息，类别，然后展开一组消息。 单击左窗格中选择的对象，并在右窗格中显示的详细信息的单个消息。  
  
## <a name="analyzing-conversion-problems-by-using-the-assessment-report"></a>使用评估报告来分析转换问题  
转换的统计信息窗格中显示的转换统计信息。 如果任何类别的百分比低于 100%，应确定为何转换未成功。  
  
**若要查看转换问题**  
  
1.  通过使用前面的过程中的说明创建评估报告。  
  
2.  在左窗格中，展开架构或具有红色错误图标的文件夹。 继续展开项，直至选择失败，转换的单个项。  
  
3.  在源窗格的顶部，单击**下一个问题**。  
  
    有问题的代码会突出显示，是目标导航窗格中的相关的代码。  
  
4.  查看任何错误消息，，然后确定你想要使用导致转换问题的对象执行操作：  
  
    -   更新在 SSMA 中的 Oracle 语法。 您可以更新过程、 函数、 触发器、 封装的函数和打包的过程的语法。 若要更新的语法，请在 Oracle 元数据资源管理器窗格中选择的对象，单击**SQL**选项卡，然后修改的 SQL 代码。 导航离开该项时，系统将提示你保存已更新的语法。 您可以查看报告的错误的对象上**报表**选项卡。  
  
    -   在 Oracle 中，可以修改 Oracle 对象以删除或修改有问题的代码。 若要将更新的代码加载到 SSMA，必须更新元数据。 有关详细信息，请参阅[连接到 Oracle 数据库&#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md)。  
  
    -   您可以从迁移中排除对象。 在中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]元数据资源管理器和 Oracle 元数据资源管理器中，清除项旁边的复选框，然后加载到对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和将数据从 Oracle 迁移。  
  
## <a name="next-step"></a>下一步  
[转换 Oracle 架构&#40;OracleToSQL&#41;](../../ssma/oracle/converting-oracle-schemas-oracletosql.md)  
  
## <a name="see-also"></a>请参阅  
[迁移的 Oracle 数据库移到 SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
