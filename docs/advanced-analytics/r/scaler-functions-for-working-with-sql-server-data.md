---
title: "用于使用 SQL Server 数据的 RevoScaleR 函数 |Microsoft 文档"
ms.custom: 
ms.date: 08/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: 5f3c9864-9c75-4688-947d-0940045b2671
caps.latest.revision: "9"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 08d8d3e6a13066aa79c96ba161e1c9d8f230e60f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="revoscaler-functions-for-working-with-sql-server-data"></a>用于使用 SQL Server 数据的 RevoScaleR 函数

本主题概述了中 RevoScaleR 提供用于使用 SQL Server 数据的主函数。

ScaleR 函数以及如何使用它们的完整列表，请参阅[Microsoft R Server](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)引用。

## <a name="create-sql-server-data-sources"></a>创建 SQL Server 数据源

以下函数允许你定义 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 数据源。 数据源对象是一个容器，它指定了连接字符串以及你需要的以表、视图或查询格式定义的数据集。 不支持存储过程调用。

+ [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata) -定义[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]数据源对象。

+ [RxOdbcData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxodbcdata) -创建其他 ODBC 数据库的数据对象。 

## <a name="perform-ddl-statements"></a>执行 DDL 语句

如果你具有对实例和数据库必需的权限，您可以从 R、 执行 DDL 语句。 以下函数使用 ODBC 调用来执行 DDL 语句或检索数据库架构。

+ `rxSqlServerTableExists`和[rxSqlServerDropTable](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdroptable) -删除[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]表，或检查是否存在的数据库表或对象

+ [rxExecuteSQLDDL](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxexecutesqlddl) -执行数据定义语言 (DDL) 命令，它定义或处理数据库对象。 此函数不能返回数据，并仅用于检索或修改对象架构或元数据。

## <a name="define-or-manage-compute-contexts"></a>定义或管理计算上下文

以下函数允许你定义新的计算上下文、切换计算上下文或者标识当前计算上下文。

+ [RxComputeContext](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxcomputecontext) - 创建计算上下文。

+ [rxInSqlServer](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinsqlserver) - 生成一个允许在 SQL Server R Services 中运行 **ScaleR** 函数的 SQL Server 计算上下文。 当前，只有 Windows 上的 SQL Server 实例支持此计算上下文。

+ `rxGetComputeContext`和[rxSetComputeContext](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetcomputecontext) -获取或设置活动计算上下文。

## <a name="move-data-and-transform-data"></a>将数据移动和转换数据

创建数据源对象后，你可以使用对象数据加载到它、 转换数据，或将新数据写入到指定的目标。 你还可以根据源中的数据大小将批大小定义为数据源的一部分，并成块移动数据。

+ [rxOpen 方法](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxopen-methods)-检查是否可用的数据源，打开或关闭数据源，从源中读取数据、 将数据写入到目标，并关闭数据源

+ [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport) -将数据从数据源移到文件存储或数据帧。

+ [rxDataStep](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep) -在移动数据源之间转换数据。

可以使用以下函数以 XDF 格式创建的本地数据存储区。 当处理的数据多于可以在一批中从数据库传输的数据时，或者数据多于内存中可以容纳的数据时，此文件可能比较有用。

例如，如果定期移动大量的数据从数据库到本地工作站，而不是查询数据库重复对于每个 R 操作中，你可以使用 XDF 文件用作一种缓存以保存本地的数据，然后使用它在 R 工作区中。

+ [RxXdfData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxxdfdata) -创建 XDF 数据对象

+ [rxReadXdf](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxreadxdf) -XDF 文件中的数据读入数据帧

有关使用这些函数的详细信息中, 包括使用数据源而非[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，请参阅[操作方法指南 Microsoft R 中的数据分析](https://docs.microsoft.com/r-server/r/how-to-introduction)。
