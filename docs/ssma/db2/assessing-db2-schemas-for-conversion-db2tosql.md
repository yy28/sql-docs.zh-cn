---
title: 评估 DB2 架构转换 (DB2ToSQL) |Microsoft 文档
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
ms.assetid: 8892f5a4-72ba-4406-8649-7a9d67f4c1d9
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 93ca9f22df0bf6e458676bd2de76f10009f67d44
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2018
ms.locfileid: "34774393"
---
# <a name="assessing-db2-schemas-for-conversion-db2tosql"></a>转换 (DB2ToSQL) 评估 DB2 架构
在加载对象并将数据迁移到之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，迁移将十分复杂和多少时间应确定将需要迁移。 SSMA 可以创建显示百分比将成功转换的对象的评估报表。 SSMA 还允许你查看的特定问题导致转换失败。  
  
## <a name="creating-assessment-reports"></a>创建评估报表  
SSMA 时它会创建此评估报告，将转换到所选的 DB2 数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]语法，然后显示结果。  
  
**创建评估报表**  
  
1.  在 DB2 元数据资源管理器，选择要评估的架构。  
  
2.  若要省略单个对象，清除那些旁边的复选框。  
  
3.  右键单击**架构**，然后选择**创建报表**。  
  
    您也可以通过右键单击对象，然后选择分析单个对象**创建报表**。  
  
    SSMA 将在窗口底部的状态栏中显示进度。 如果输出窗格可见时，你还将看到输出窗格中的消息。  
  
    评估完成后， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant for DB2： 将出现评估报表窗口。  
  
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
  
    -   更新中 SSMA 的 DB2 语法。 你可以更新过程、 函数、 触发器、 打包的函数和打包的过程的语法。 若要更新的语法，在 DB2 元数据资源管理器窗格中选择的对象，请单击**SQL**选项卡上，然后修改的 SQL 代码。 离开项时，系统将提示你保存已更新的语法。 你可以查看对象报告的错误上**报表**选项卡。  
  
    -   在 DB2，你可以修改要删除或修改有问题的代码的 DB2 对象。 若要更新的代码载入 SSMA，你将需要更新的元数据。 有关详细信息，请参阅[连接到 DB2 数据库&#40;DB2ToSQL&#41;](../../ssma/db2/connecting-to-db2-database-db2tosql.md)。  
  
    -   你可以从迁移中排除对象。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]元数据资源管理器和 DB2 元数据资源管理器中，清除项旁边的复选框，在加载到对象之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]从 DB2 中迁移数据。  
  
## <a name="next-step"></a>下一步  
[转换 DB2 架构&#40;DB2ToSQL&#41;](../../ssma/db2/converting-db2-schemas-db2tosql.md)  
  
## <a name="see-also"></a>请参阅  
[迁移 DB2 数据库移到 SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  
