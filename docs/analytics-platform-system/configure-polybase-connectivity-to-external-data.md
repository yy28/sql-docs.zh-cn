---
title: 配置 PolyBase 连接-分析平台系统 |Microsoft Docs
description: 介绍如何在并行数据仓库，若要连接到外部 Hadoop 或 Microsoft Azure 存储 blob 数据源中配置 PolyBase。 使用 PolyBase 将运行集成来自多个源，包括 Hadoop、 Azure blob 存储和并行数据仓库的数据的查询。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: da6d71521f72ff23b4caf2f27dbc663dee684592
ms.sourcegitcommit: 5afec8b4b73ce1727e4e5cf875d1e1ce9df50eab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2018
ms.locfileid: "47450292"
---
# <a name="what-is-polybase"></a>什么是 PolyBase？
PolyBase 使可以处理可以从中读取数据并将数据写入到外部数据源的 TRANSACT-SQL 查询在 Analytics Platform System (APS)。 访问外部数据的相同查询还可以在您的 AP 中包含的关系表。 这样即可将数据从外部源与高价值 APS 数据库中的关系数据合并。

![PolyBase 逻辑](media/polybase/polybase-logical.png)

AP 上的 PolyBase 支持读取和写入到 Hadoop (HDFS) 文件系统和 Azure Blob 存储。 PolyBase 还能够将某些计算推送到 Hadoop 节点，作为 mapreduce 作业，以优化总体查询性能。 PolyBase AP 上的可以对分隔的文本、 ORC 和 Parquet 文件。 请参阅[什么是 PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)实现的完整说明和其功能。

> [!NOTE]
> APS 目前仅支持标准常规用途 v1 本地冗余 (LRS) Azure Blob 存储。

## <a name="features-and-limitations"></a>功能和限制
请参阅[功能和限制](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-versioned-feature-summary)的 PolyBase 摘要特色 APS 和其他 SQL Server 产品的可用和已知限制的。

> [!NOTE] 
> 在 PolyBase 的其余部分相关的文章介绍如何配置 PolyBase APS 2016 (AU6) 及更高版本。

## <a name="see-also"></a>请参阅
- [Hadoop](polybase-configure-hadoop.md)
- [Azure Blob 存储](polybase-configure-azure-blob-storage.md)
<!-- MISSING LINKS [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md)  -->  
  
