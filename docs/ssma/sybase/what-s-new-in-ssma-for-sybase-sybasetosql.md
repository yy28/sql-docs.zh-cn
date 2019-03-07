---
title: 什么是适用于 SAP ASE (SybaseToSQL) 的 SSMA 中的新增功能 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2be0cf8d-6dbe-443a-abbd-036249922205
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 875f89a53963633a267ada1ae1563360cbebf7d8
ms.sourcegitcommit: d7ed341b2c635dcdd6b0f5f4751bb919a75a6dfe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57527090"
---
# <a name="whats-new-in-ssma-for-sap-ase-sybasetosql"></a>什么是适用于 SAP ASE (SybaseToSQL) 的 SSMA 中的新增功能
本文列出了每个版本中的 SAP ASE (以前称为 SSMA for Sybase) 更改 SQL Server Migration Assistant (SSMA)。

## <a name="ssma-v81"></a>SSMA v8.1
有关 SAP ASE 的 SSMA v8.1 发布已增强，旨在提高质量和转换的度量值的目标修补。

> [!NOTE]
> 自动更新的已知的问题可能会导致失败的更新从 SSMA v8.0 v8.1。 如果遇到此错误，请下载最新版本，然后手动安装它。

> [!IMPORTANT]
> 使用 SSMA v7.4 和更高版本，.Net 4.5.2 是安装必备组件。

## <a name="ssma-v80"></a>SSMA v8.0
有关 SAP ASE 的 SSMA v8.0 发布已增强，设计用于提高质量和转换的度量值的目标修补。 此外，此版本提供了以下新功能：

* 为支持**Azure SQL 数据库托管实例**作为目标。 现在可以创建目标 Azure SQL 数据库托管实例的新项目：

    ![SQL DB MI 项目](../media/ssma-newproject-sqldbmi.png)

*   转换后**修复顾问**。 了解有关它的详细信息[此处](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/)。

*   初步的数据库架构所选内容。

    连接到源时，用户现在可以选择感兴趣的数据库/架构。 选择你打算迁移的架构将保存在初始连接期间的时间并改进整体 SSMA 性能。

    ![SSMA 筛选对象](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v7.10
有关 SAP ASE 的 SSMA v7.10 发布已增强，可提供额外的安全和隐私保护功能以满足全局要求中的更改的目标修补。

## <a name="ssma-v79"></a>SSMA v7.9
SAP ASE 的 SSMA v7.9 发行版包含以下更改：
- 提高质量和转换的度量值的目标的修补。
- 支持在 SSMA 命令行中更改数据类型映射和项目首选项。
- 有关迁移支持使用 SQL Server Integration Services (SSIS) 数据。 转换后的架构，则可以通过右键单击上下文菜单选项创建的 SSIS 包。
- SSMA 中的 Azure SQL 数据库连接对话框也已更改，以指定完全限定的服务器名称。 在以前版本的 SSMA，Azure SQL 数据库前缀必须明确指出在项目设置。

## <a name="ssma-v78"></a>SSMA v7.8
SAP ASE 的 SSMA 7.8 版发行版包含以下更改：
- 更改项目设置中突出显示的类型映射。
- 用户若要禁用遥测数据的能力。

## <a name="ssma-v77"></a>SSMA v7.7
SAP ASE 的 SSMA v7.7 发行版包含以下更改：
- 适用于 SAP ASE 的 SSMA 已得到增强改进质量和转换的度量值的目标修补。
- 基于普遍的需求，返回是适用于 SAP ASE 的 SSMA 的 32 位版本。 相比以前的实现 (之前为 v7.4)，有两个安装程序软件包，但不能并行安装。 因此，必须选择最适合您的版本根据连接组件。 最好始终使用 64 位版本中，在可能的情况。

## <a name="ssma-v76"></a>SSMA v7.6
SAP ASE 的 SSMA v7.6 发行版包含以下更改：
- 针对提高质量和转换的度量值的修补程序和对 SQL Server 2017 （公共预览版） 的支持。 支持 Windows 和 Linux 上的 SQL Server 2017 处于公共预览状态，不应该用于生产迁移。
- 支持 Sybase 函数转换。

## <a name="ssma-v75"></a>SSMA v7.5
SSMA for SAP ASE (以前称为 SSMA for Sybase) 的版本 7.5 版本包含以下更改：
-   若要确保为残障人士使用的可访问性的多项改进。
-   创建或替换语法的支持。

## <a name="ssma-v74"></a>SSMA v7.4
SSMA for Sybase 的 v7.4 版本包含以下更改：
- **查询超时值**选项现可在源和目标架构对象发现期间访问。

    ![query timeout 选项](../media/query-timeout_red.png)
- 有所改进质量和转换指标，包括目标修补，根据客户反馈。

> [!IMPORTANT]
> .Net 4.5.2 是用于安装 SSMA v7.4 必备组件。 此外，从 v7.4 开始，SSMA 的 32 位版本正在停止。  

## <a name="ssma-v73"></a>SSMA v7.3
SSMA for Sybase 的 v7.3 版本包含以下更改：
- 改进的质量和转换度量值与目标修补，根据客户反馈。
- 通过以下各项公开的 SSMA 可扩展性框架：
  - 导出到 SQL Server Data Tools (SSDT) 项目的功能。
    -   现在，您可以到 SSDT 项目从 SSMA 导出架构脚本。 架构脚本可用于进行附加的架构更改和部署你的数据库。

        ![将另存为 SSDT 项目命令](../media/export-schema-scripts_red.png)
  - 可供执行的自定义转换 SSMA 的库。
    - 现在可以构造自定义语法转换和转换之前未处理的 SSMA 能处理的代码。
      - 在此博客文章提供了有关如何构造自定义转换器说明[扩展 SQL Server Migration Assistant 的转换功能](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)。
      - 下载此转换的示例项目[博客文章](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/)。

## <a name="ssma-v72"></a>SSMA v7.2
SSMA for Sybase 的 7.2 版版本包含以下更改：
- 改进的质量和转换度量值与目标修补，根据客户反馈。
- 遥测数据增强功能提供更好的数据点来解决客户问题并提高 SSMA 的转换率。

## <a name="ssma-v71"></a>SSMA v7.1
SSMA for Sybase 的 v7.1 版本包含以下更改：
- SQL Server 2017 的 Windows 和 Linux CTP1 现在是用于迁移的支持的目标平台。 此功能在 technical preview 中，支持架构和数据移动到目标 SQL 服务器。
- 若要下载最新版本的 SSMA 立即可用的自动更新的支持。
- SSMA 可安装二进制文件现在被通过 Windows installer 包文件 (.msi)。

**资源**

[扩展 SQL Server Migration Assistant 的转换功能](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)

[评估并将数据从非 Microsoft 数据平台迁移到 SQL Server *（与 Oracle 的示例）*](https://blogs.msdn.microsoft.com/datamigration/2016/11/16/sql-server-migration-assistant-how-to-assess-and-migrate-databases-from-non-microsoft-data-platforms-to-sql-server/) 

## <a name="may-2016"></a>2016 年 5 月  
SSMA for Sybase 的 2016 年 5 月版本包含以下更改：  

-  添加了对 SQL Server 2016 的支持。
-  删除.Net 2.0 的安装程序检查。
-  已更新的扩展包依赖项从.Net 3.5 到.Net 4.0。
-  修复了"保存项目"和 SSMA 控制台的"打开项目"命令。
-  SSMA 控制台中的固定"securepassword"命令。
-  修复了初始加载的对象的计数。
-  全局设置中修复了 bug。

## <a name="march-2016"></a>2016 年 3 月  
Sybase 的 SSMA 的 2016 年 3 月预览版本将对迁移的支持添加到 SQL Server 2016。  
  
## <a name="january-2016"></a>2016 年 1 月  
Sybase 的 SSMA 的 2016 年 1 月维护版本包含以下更改：  
  
-  SSMA (RFC 5706203) 添加了的视图日志菜单项。  
-  添加了遥测数据。 
  
## <a name="july-2014"></a>2014 年 7 月  
SSMA for Sybase 的 2014 年 7 月版本包含以下更改：  
  
-  改进了的 Azure SQL DB 代码转换。  
-  移动到架构以支持 Azure SQL DB 扩展包功能。  
-  添加了的性能改进测试具有超过 10 k 的数据库对象。  
-  添加了的大量对象处理的 UI 改进。  
-  添加突出显示"已知"LOB 架构 （因此也可以在转换过程中忽略） 的功能。  
-  添加转换速度改进。  
-  添加在用户界面中显示对象计数的功能。 
-  降低的报表大小的 25%以上。  
-  未分析的构造的改进的错误消息。  
  
## <a name="april-2014"></a>2014 年 4 月  
SSMA for Sybase 的 2014 年 4 月版本包含以下更改：  
  
-   MS SQL Server 2014 添加了的支持。  
-   有关转换到 Azure 的已修复的 bug。  
-   有关 IE 10 中的不可见的报表页的已修复的 bug。  
  
## <a name="january-2012"></a>2012 年 1 月  
SSMA for Sybase 的 2012 年 1 月版本包含以下更改：  
  
-   添加了的对回滚触发器转换。  
-   为转换提供修复 @@ROWCOUNT 和 @@ERROR 在同一组语句。  
  
## <a name="july-2011"></a>2011 年 7 月  
SSMA for Sybase 的 2011 年 7 月版本提供了改进的数据迁移期间报告的错误。  
  
## <a name="april-2011"></a>2011 年 4 月  
SSMA for Sybase 的 2011 年 4 月版本包含以下更改：  
  
-   合并"Sybase 的 SSMA"产品，它支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005 中， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali"和 Azure SQL。  
-   添加了对连接和迁移到支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]"Denali"。  
-   添加用于将转换并迁移到 Azure SQL 的 Sybase 数据库的新功能。  
-   增强的客户端的数据迁移引擎，支持并行迁移的数据。  
-   改进的数据迁移性能与简单和大容量日志恢复模式。  
-   添加正确转换和区分大小写的 Sybase 数据库迁移到区分大小写的 SQL Server 的功能。  
-   添加了对转换 Sybase ASE 非 ANSI 联接语句的 SQL Server ANSI 联接语句的支持已扩展为删除和更新语句。  
-   提供用于连接到 Sybase ASE 服务器使用 Sybase ASE ODBC 访问接口和 Sybase ASE ADO.Net 提供程序的其他连接选项。  
-   删除对名为的单独数据库的依赖关系**SysDB**，其中包含 Sybase 仿真函数 （作为扩展包的一部分安装）。  
-   添加了安装 SSMA for Sybase 的扩展包上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]群集。  
-   添加了向后兼容性的 SSMA （版本 4.0 和 4.2 版） 的早期版本创建的项目。  
-   添加了使用较旧版本的 SSMA （版本 4.0 和 4.2 版） 安装 SSMA for Sybase 5.0 版产品的并行 (SxS)。  
  
## <a name="july-2010"></a>2010 年 7 月  
SSMA for Sybase 的 2010 年 7 月版本包含以下更改：  
  
-   添加了对迁移到 SQL Server 2008 R2 的支持。  
-   添加新命令行执行的 SSMA 控制台应用程序。  
-   添加了的对使用服务器端和客户端的数据迁移引擎数据迁移。  
-   添加了的对"自定义选择"在数据迁移的语句。  
-   添加了的对从 Sybase ASE 15.0.3 和 15.5 迁移。  
  
## <a name="june-2008"></a>2008 年 6 月  
SSMA for Sybase 的 2008 年 6 月版本包含以下更改：  
  
-   添加了的 SSMA Tester，自动测试的数据库对象转换，以及所做的 SSMA 在数据迁移。 在完成所有的 SSMA 迁移步骤后，使用 SSMA 测试人员验证已转换的对象相同的方式工作，所有数据已正确都传输。  
-   添加的预 SQL 转换。 用户现在可以指定临时表 （和其他对象） 要在转换中使用的每个源过程的声明。  
-   添加了对象转换中的改进：  
    -   联接修订的转换。  
    -   聚合和非聚合而无需具有/组 by 子句。  
    -   SELECT INTO 语句使用 IDENTITY 函数。  
    -   聚集的约束和索引的数据仅锁定。  
    -   由 SELECT INTO 创建的临时表。  
    -   约束 / 临时表的索引。  
    -   新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]支持 2008 datetime 类型。  
    -   Sybase 15.0 连接和数据类型支持。  
  
## <a name="may-2007"></a>2007 年 5 月  
SSMA for Sybase 的 2007 年 5 月版本包含以下更改：  
  
-   添加保存项目时更快地加载数据库内容的功能。  
-   添加了的对 SQL Server 中的用户输入注释格式 SQL 模式。  
-   添加了对象转换中的改进。  
  
对于此版本不被更新的帮助文件。 有关详细信息，请参阅本文后面的文档说明部分。  
  
## <a name="november-2006"></a>2006 年 11 月  
SSMA for Sybase 的 2006 年 11 月版本包含以下更改：  
  
-   添加新的全局设置：  
    -   您可以选择在编辑器窗口中显示行号。  
    -   你可以配置 SSMA 提示以替换重复的对象，或始终或永远不会将重复的对象为架构转换过程。  
-   添加新的转换选项，允许你配置如何 SSMA 处理以下情况：  
    -   包含二进制字符串的 CAST 或 CONVERT 语句。  
    -   检查相等表达式中的 null 值。  
    -   代理表。  
    -   RAISERROR 的用户消息错误号。  
    -   包含无法解析的标识符的 UPDATE 语句。  
-   添加新的迁移选项，允许您指定 SSMA 应如何处理日期外部[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]日期范围。  
-   添加**格式化 SQL**上设置**SQL**选项卡上，后者将格式设置以改善可读性的代码。  
-   Bug 修复，包括：  
    -   SSMA 现在将转换的锁表*表*IN {共享 |通过将 TABLOCK 或 TABLOCKX 提示添加到后续的 SELECT 查询对表的排他} 模式语句。  
    -   在字符表达式中使用二进制类型时，现在已添加必要的强制转换。  
    -   内存和性能改进。  
  
## <a name="july-2006"></a>2006 年 7 月  
2006 年 7 月发布的用于 Sybase 的 SSMA 是初次发布。  
  
## <a name="see-also"></a>请参阅  
[开始使用 SSMA for Sybase &#40;SybaseToSQL&#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)
