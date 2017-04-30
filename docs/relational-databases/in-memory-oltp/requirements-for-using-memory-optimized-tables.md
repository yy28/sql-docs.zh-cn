---
title: "使用内存优化表的要求 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 11/16/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 47d9a7e8-c597-4b95-a58a-dcf66df8e572
caps.latest.revision: 65
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d30c5b808c13258e784187182eab23b0a50c76e0
ms.lasthandoff: 04/11/2017

---
# <a name="requirements-for-using-memory-optimized-tables"></a>使用内存优化表的要求
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  若要了解如何在 Azure DB 中使用内存中 OLTP，请参阅 [Get started with In-Memory in SQL Database](http://azure.microsoft.com/documentation/articles/sql-database-in-memory/)（在 SQL 数据库中使用内存中功能入门）。  
  
 除了需要满足 [安装 SQL Server 2016 的硬件和软件要求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)外，还要满足以下使用内存中 OLTP 的要求：  
  
-   SQL Server 2016 SP1（或更高版本），任何版本。 对于 SQL Server 2014 和 SQL Server 2016 RTM（SP1 预览版），需要 Enterprise、Developer 或 Evaluation 版。
    - 注意：内存中 OLTP 要求 64 位版本的 SQL Server。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 需要有足够的内存来保留内存优化表和索引中的数据，以及额外的内存来支持联机工作负荷。 有关详细信息，请参阅 [估算内存优化表的内存需求](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md) 。  

-   在虚拟机 (VM) 中运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时，请确保有足够的内存分配给 VM 以提供内存优化表和索引所需的内存。 用于保证 VM 内存分配的配置选项可称为“内存预留”或“最小 RAM”（使用动态内存时），具体取决于 VM 主机应用程序。 请确保这些设置足以满足 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的数据库需求。
  
-   可用磁盘空间需为你的持久内存优化表大小的两倍。  
  
-   处理器必须支持指令 **cmpxchg16b** 才能使用内存中 OLTP。 所有新式 64 位处理器都支持 **cmpxchg16b**。  
  
     如果你使用的是虚拟机，并且 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 显示因处理器较旧而生成的错误消息，请检查虚拟机主机应用程序是否将配置选项设置为允许使用 **cmpxchg16b**。 如果没有设置，你可以使用支持 **cmpxchg16b** 的 Hyper-V，而无需修改配置选项。  
  
-   内存中 OLTP 作为 **数据库引擎服务**的一部分进行安装。  
  
     要安装报表生成（[确定表或存储过程是否应移植到内存中 OLTP](../../relational-databases/in-memory-oltp/determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md)）和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] （通过 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 对象资源管理器管理内存中 OLTP）， [请下载 SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx)。  
  
## <a name="important-notes-on-using-includehek2includeshek-2-mdmd"></a>有关使用 [!INCLUDE[hek_2](../../includes/hek-2-md.md)]的重要说明  
  
-   启动 SQL Server 2016 时，对内存优化表的大小没有限制（不同于可用内存）。 SQL Server 2014 数据库中所有持久表的内存中总大小不应超过 250 GB。 有关详细信息，请参阅 [估算内存优化表的内存需求](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md)。  
    - 注意：从 SQL Server 2016 SP1 开始，Standard 和 Express 版本支持内存中 OLTP，但它们对可用于给定数据库中内存优化表的内存量设置了配额。 在 Standard 版本中，每个数据库的配额是 32GB；在 Express 版本中，每个数据库的配额是 352MB。 
  
-   如果创建一个或多个包含内存优化表的数据库，应对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例启用即时文件初始化（授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务启动帐户 SE_MANAGE_VOLUME_NAME 用户权限）。 如果没有即时文件初始化，内存优化存储文件（数据和差异文件）将在创建时初始化，这会对工作负荷性能产生负面影响。 有关即时文件初始化的详细信息，请参阅 [数据库文件初始化](http://msdn.microsoft.com/library/ms175935\(SQL.105\).aspx)。 有关如何启用即时文件初始化的信息，请参阅 [启用即时文件初始化的方法和原因](http://blogs.msdn.com/b/sql_pfe_blog/archive/2009/12/23/how-and-why-to-enable-instant-file-initialization.aspx)。  
  
## <a name="see-also"></a>另请参阅  
 [内存中 OLTP（内存中优化）](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  

