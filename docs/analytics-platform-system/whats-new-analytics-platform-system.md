---
title: 什么是分析平台系统 – 向外扩展数据仓库中的新增功能
author: happynicolle
ms.author: nicw;barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: ''
ms.technology: mpp-data-warehouse
description: 请参阅什么是 Microsoft® 分析平台系统中的新增、 横向扩展本地承载 MPP SQL Server 并行数据仓库的设备。
ms.date: 11/28/2016
ms.topic: article
ms.openlocfilehash: c6af71d6b7c2bc67aeea0fdc5c1af2e668f537c5
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="whats-new-in-analytics-platform-system-2016-a-scale-out-mpp-data-warehouse"></a>什么是分析平台系统 2016，向外扩展 MPP 数据仓库中的新增功能
请参阅什么是在 Microsoft® 分析平台系统 (AP) 2016年新、 最新的横向扩展的设备更新本地承载 MPP SQL Server 并行数据仓库的设备。 

## <a name="sql-server-2016"></a>SQL Server 2016

AP 2016 在最新的 SQL Server 2016 版本上运行，并使用默认数据库兼容性级别 130。  SQL Server 2016 使可以为 PolyBase 支持的一些新功能，例如辅助索引的聚集列存储索引和 Kerberos。 


## <a name="t-sql"></a>T-SQL
AP 2016 支持这些 T-SQL 兼容性改进。  这些其他语言元素更加轻松地从 SQL Server 和其他数据源迁移。 

- [列级 SQL 排序规则][]现在支持除了 Windows 排序规则。
- [聚集列存储索引的非聚集索引][]改进搜索聚集列存储索引中的特定值的查询性能。 
- [SELECT...INTO][] 
- [sp_spaceused()][]显示磁盘空间使用，或保留表或数据库中。
- [宽表][]支持等同于 SQL Server 2016。 行大小以前限制为 32k 不再存在。 

### <a name="data-types"></a>数据类型

- [Varchar （max)][]， [nvarchar (MAX)][]和[varbinary （max)][]。 这些 LOB 数据类型的最大为 2 GB。 若要加载这些对象，请使用[bcp 实用工具][]。 Polybase 和 dwloader 当前不支持这些数据类型。 
- [SYSNAME][]
- [UNIQUEIDENTIFIER][]
- [数值][]和十进制数据类型。

### <a name="window-functions"></a>开窗函数

- [ROWS 或 RANGE][] OVER 子句的 SELECT 语句中。
- [FIRST_VALUE][]
- [LAST_VALUE][]
- [CUME_DIST][]
- [PERCENT_RANK][]

### <a name="security-functions"></a>安全函数

- [使 checksum （)][]和[BINARY_CHECKSUM()][]
- [HAS_PERMS_BY_NAME()][]

### <a name="additional-functions"></a>其他函数

- [NEWID()][]
- [RAND()][]

## <a name="polybasehadoop-enhancements"></a>PolyBase/Hadoop 增强功能

- 与 Hortonworks HDP 2.4 和 HDP 2.5 兼容性
- Kerberos 支持通过数据库范围凭据
- Azure 存储 blob 的凭据支持

## <a name="install-and-upgrade-enhancements"></a>安装和升级的增强功能

### <a name="enterprise-architecture-updates"></a>企业体系结构更新
将你的现有设备升级到 AP 2016 安装最新的固件和驱动程序更新，包括安全修补程序。 

一个新的设备从 HPE 或 DELL 包括所有最新的更新以及：

- 最新生成处理器支持 (Broadwell)
- 更新到 DDR4 Dimm
- 改进了的 DIMM 吞吐量

### <a name="integration"></a>集成

- 完全限定域名 (FQDN) 支持使可以安装到设备的域信任。 
- 若要使用 FQDN，你需要执行完整的升级，并选择在升级过程。 

### <a name="reduced-downtime"></a>减少了停机时间
安装或升级到 AP 2016 速度更快且需要比以前的版本中减去停机时间。 若要降低停机时间、 安装或升级： 

 - 通过使用包含通过 2016 年 6 月的所有更新的映像应用 WSUS 更新的优化
 - 适用的驱动程序和固件更新的安全更新
 - 这样便已准备好安装，也无需下载它们会在你的设备上的最新修补程序和设备验证实用程序 (PAV)。


<!--MSDN references-->
[database compatibility level 130]:https://msdn.microsoft.com/library/bb510680.aspx
[列级 SQL 排序规则]:https://msdn.microsoft.com/library/ms143726.aspx
[聚集列存储索引的非聚集索引]:https://msdn.microsoft.com/library/ms188783.aspx
[Varchar （max)]:https://msdn.microsoft.com/library/ms176089.aspx
[nvarchar (MAX)]:https://msdn.microsoft.com/library/ms186939.aspx
[varbinary （max)]:https://msdn.microsoft.com/library/ms188362.aspx
[SYSNAME]:https://msdn.microsoft.com/library/ms188021.aspx
[SELECT...INTO]:https://msdn.microsoft.com/library/ms188029.aspx
[sp_spaceused()]:https://msdn.microsoft.com/library/ms188776.aspx
[宽表]:https://msdn.microsoft.com/library/ms143432.aspx
[BULK INSERT]:https://msdn.microsoft.com/library/ms188365.aspx
[bcp 实用工具]:https://msdn.microsoft.com/library/ms162802.aspx
[UNIQUEIDENTIFIER]:https://msdn.microsoft.com/library/ms187942.aspx
[数值]:https://msdn.microsoft.com/library/ms187746.aspx
[ROWS 或 RANGE]:https://msdn.microsoft.com/library/ms189461.aspx
[FIRST_VALUE]:https://msdn.microsoft.com/library/hh213018.aspx
[LAST_VALUE]:https://msdn.microsoft.com/library/hh231517.aspx
[CUME_DIST]:https://msdn.microsoft.com//library/hh231078.aspx
[PERCENT_RANK]:https://msdn.microsoft.com/library/hh213573.aspx
[使 checksum （)]:https://msdn.microsoft.com/library/ms189788.aspx
[BINARY_CHECKSUM()]:https://msdn.microsoft.com/library/ms173784.aspx
[HAS_PERMS_BY_NAME()]:https://msdn.microsoft.com/library/ms189802.aspx
[NEWID()]:https://msdn.microsoft.com/library/ms190348.aspx
[RAND()]:https://msdn.microsoft.com/library/ms177610.aspx


  

  


