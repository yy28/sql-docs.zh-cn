---
title: 转换 Sybase ASE 数据库对象 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 12/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Converting Database Objects
ms.assetid: 509cb65d-2f54-427a-83d7-37919cc4e3e3
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 9298a094187b38cf005928dfc4832fc529222b1b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47601777"
---
# <a name="converting-sap-ase-database-objects-sybasetosql"></a>转换 SAP ASE 数据库对象 (SybaseToSQL)
连接到 SAP Adaptive Server Enterprise (ASE) 后，连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL 和将项目设置和数据映射选项，可以将转换为 SAP Adaptive Server Enterprise (ASE) 数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL 数据库对象。  
  
## <a name="the-conversion-process"></a>转换过程  
将转换数据库对象从 ASE 所需的对象定义、 将其转换为类似[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 对象，再然后将此信息加载到 SSMA 元数据。 它不到的实例加载信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL。 您然后可以通过查看对象和其属性[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL 元数据资源管理器。
  
在转换期间 SSMA 将打印消息输出到输出窗格和错误消息为**错误列表**窗格。 使用的输出和错误的信息来确定是否必须修改 ASE 数据库或转换过程来获取所需的转换结果。  
  
## <a name="setting-conversion-options"></a>设置转换选项  
在将对象转换之前, 查看中的项目转换选项**项目设置**对话框。 通过使用此对话框中，可以设置 SSMA 将函数和全局变量的转换。 有关详细信息，请参阅[项目设置&#40;转换&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md)。  
  
## <a name="converting-ase-database-objects"></a>转换 ASE 数据库对象  
若要转换 ASE 数据库对象，首先选择想要转换的对象，然后执行转换的 SSMA。 若要在转换期间查看输出消息上**视图**菜单中，选择**输出**。  
  
**若要将 ASE 对象转换为 SQL Server 或 SQL Azure 的语法**  
  
1.  Sybase 元数据资源管理器中展开 ASE 服务器，然后展开**数据库**。  
  
2.  选择要转换的对象：  
  
    -   若要将所有数据库，选择复选框旁边**数据库**。  
  
    -   若要将转换或省略数据库，选择或清除的数据库名称旁边的复选框。  
  
    -   若要将转换或省略的单个架构，展开数据库，展开**架构**，然后选中或清除架构旁边的复选框。  
  
    -   若要将转换或忽略的对象的类别，展开架构，然后选择或清除类别旁边的复选框。  
  
    -   若要将转换或忽略各个对象，展开类别文件夹，然后选择或清除的对象旁边的复选框。  
  
3.  若要将所有选定的对象的转换，请右键单击**数据库**，然后选择**转换架构**。  
  
    您还可以通过右键单击该对象或其包含的文件夹，然后选择转换单个对象的类别**转换架构**。  
  
> [!NOTE]  
> SAP ASE 系统函数的一些不完全匹配等效的 SQL Server 系统函数的行为。 若要模拟的 SAP ASE 行为，SSMA 下名为 s2ss 的架构转换后的 SQL Server 数据库中生成用户定义的函数。 具体取决于项目设置中，某些 SQL Server 系统函数会替换这些仿真函数。 SSMA 会创建以下用户定义函数：  
  
||||  
|-|-|-|  
|**char_length_nvarchar**|**index_colorder**|**ssma_datepart**|  
|**char_length_varchar**|**inttohex**|**substring_nvarchar**|  
|**charindex_nvarchar**|**ssma_datediff**|**substring_varbinary**|  
|**charindex_varchar**|**hextoint**|**substring_varchar**|  
|**ulowsurr**|**to_unichar**|**ssma_current_time**|  
|**uhighsurr**|||  
  
## <a name="objects-not-supported-in-azure-sql"></a>不支持在 Azure SQL 中的对象  
下面的 T-SQL 关键字由 SSMA for SAP ASE 期间转换为 SQL Server 的本地，但这些关键字不受 SQL Azure T-SQL 语法：  
  
||||  
|-|-|-|  
|CHECKPOINT|CREATE/ALTER/DROP DEFAULT|CREATE/DROP RULE|  
|DBCC TRACEOFF|DBCC TRACEON|GRANT/REVOKE/DENY ALL|  
|KILL|READTEXT|SELECT INTO|  
|SET OFFSETS|SETUSER|SHUTDOWN|  
|WRITETEXT|||  
  
## <a name="viewing-conversion-problems"></a>查看转换问题  
SAP ASE 的某些对象可能不进行转换。 您可以查看摘要转换报告来确定转换成功率。  
  
**若要查看摘要报表**  
  
1.  在 Sybase 元数据资源管理器中，选择**数据库**。  
  
2.  在右窗格中，选择**报表**选项卡。  
  
    此报表显示所有数据库对象的已评估或转换摘要评估的报表。 你还可以查看摘要报告为单个对象：  
  
    -   若要查看单个数据库的报表，请在 Sybase 元数据资源管理器中选择的数据库。  
  
    -   若要查看一个单独的数据库对象的报表，请在 Sybase 元数据资源管理器中选择的对象。 具有转换问题的对象都有红色错误图标。  
  
对于无法转换的对象，可以查看导致转换失败的语法。  
  
**若要查看单个转换问题**  
  
1.  在 Sybase 元数据资源管理器中，展开**数据库**。  
  
2.  展开显示红色错误图标的数据库。  
  
3.  展开**架构**文件夹，然后展开显示红色错误图标的架构。  
  
4.  在架构中，展开具有红色错误图标的文件夹。  
  
5.  选择具有红色错误图标的对象。  
  
6.  在右窗格中，选择**报表**选项卡。  
  
7.  在顶部**报表**选项卡是一个下拉列表。 如果列表中显示**统计信息**，更改到所选**源**。  
  
    SSMA 显示的源代码和几个按钮，上面的代码。  
  
8.  选择**下一个问题**，其箭头指向右侧红色错误图标。  
  
    适用于 SAP ASE 的 SSMA 将突出显示第一个有问题的源代码的当前对象中找到。  
  
对于无法转换每个项，您需要确定想要使用该对象执行操作：  
  
-   您可以在编辑过程和触发器的源代码**SQL**选项卡。  
  
-   您可以更改要删除或修改有问题的代码的 SAP ASE 对象。 若要将更新的代码加载到 SSMA，必须更新元数据。 有关详细信息，请参阅[连接到 SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md)。  
  
-   您可以从迁移中排除对象。 在中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL 元数据资源管理器和 Sybase 元数据资源管理器中，加载到对象之前清除项旁边的复选框[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL 和数据从 SAP ASE 迁移。  
  
## <a name="next-steps"></a>后续步骤  
迁移过程中的下一步是[加载到 SQL Server 转换数据库对象 / SQL Azure (SybaseToSQL)](http://msdn.microsoft.com/4c59256f-99a8-4351-9559-a455813dbd06)。  
  
## <a name="see-also"></a>另请参阅  
[SAP ASE 数据库迁移到 SQL Server-Azure SQL 数据库&#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
