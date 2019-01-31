---
title: PolyBase 中的常见问题解答 |Microsoft Docs
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: polybase
ms.topic: conceptual
author: Abiola
ms.author: aboke
manager: ''
ms.openlocfilehash: 331ac177831b1e07cfab253c363a35f2bab42a6c
ms.sourcegitcommit: ee76381cfb1c16e0a063315c9c7005f10e98cfe6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2019
ms.locfileid: "55072873"
---
# <a name="frequently-asked-questions"></a>常见问题

## <a name="polybase-in-big-data-clusters-vs-polybase-in-stand-alone-instances"></a>大数据群集中的 PolyBase 与 独立实例中的 PolyBase

|功能 |大数据群集| 独立实例|
|--------------------------|--------------------------|---------|   
|创建外部表| X| X|
|从 SQL Server、Oracle、Teradata 和 Mongo DB 创建外部数据源 |X|X |
|使用可兼容的第三方 ODBC 驱动程序创建外部数据源 | | X|
|PolyBase 横向扩展组 | X | |
|数据池实例 | X| |
|存储池实例| X| |

>[!NOTE]
>
>有关使用 ODBC 泛型连接器进行连接的详细信息，请访问我们的[配置 ODBC 泛型类型的操作指南](polybase-configure-odbc-generic.md)

## <a name="whats-new-with-polybase-in-sql-server-2019"></a>SQL Server 2019 中 PolyBase 有什么新功能？ 

SQL Server 2019 中的 PolyBase 现可从更多种数据源读取数据。 这些外部数据源中的数据可作为外部表存储在 SQL Server 上。 PolyBase 还支持对这些外部数据源进行下推计算（不包括 ODBC 泛型类型）。 

### <a name="compatible-data-sources"></a>兼容的数据源

- SQL Server
- Oracle
- Teradata
- MongoDB
- 兼容的 ODBC 泛型类型

  > [!NOTE]
  >
  >PolyBase 可允许使用第三方 ODBC 驱动程序连接到外部数据源。 这些驱动程序不随 PolyBase 一起提供，可能按预期工作。 有关详细信息，请参阅有关 PolyBase ODBC 泛型配置的[指南](polybase-configure-odbc-generic.md)。  

## <a name="polybase-vs-linked-servers"></a>PolyBase 与 链接服务器

|PolyBase | 链接服务器|
|--------------------------|--------------------------|  
|数据库范围的对象|实例范围的对象| 
|使用 ODBC 驱动程序|使用 OLEDB 提供程序| 
| 仅支持只读操作。 以后将展开| 仅支持只读操作。 以后将展开| 
|可将查询横向扩展并支持下推|查询为单线程的并支持下推|
|Always On 可用性组不需要单独配置|Always On 可用性组中的每个实例均需要单独配置|
|仅基本身份验证。 SQL Server 2019 中的改进|基本身份验证和集成身份验证|