---
title: 宽 World Importers 文档 |Microsoft 文档
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: ''
ms.component: samples
ms.technology:
- samples
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 17cabd9d-cb2f-436c-ad9c-ce02225808b7
caps.latest.revision: 3
author: BarbKess
ms.author: barbkess
manager: craigg
robots: noindex,nofollow
ms.workload: On Demand
ms.openlocfilehash: 99d3bf3913b620a34e284b8277e4c639ba20727a
ms.sourcegitcommit: 094c46e7fa6de44735ed0040c65a40ec3d951b75
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/07/2018
---
# <a name="wide-world-importers-documentation"></a>宽 World Importers 文档
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Wide World Importers 是 SQL Server 2016 的新示例数据库和 Azure SQL 数据库。 它阐释了 SQL Server 2016 和 Azure SQL 数据库的事务处理 (OLTP)、 数据仓库和分析 (OLAP) 工作负荷，以及混合事务和分析处理 (HTAP) 工作负荷的核心功能。

## <a name="about-this-sample"></a>有关此示例

Wide World importers 计划是一个全面的数据库示例，同时说明了数据库设计，并说明了如何可以在应用程序中利用 SQL Server 功能。

请注意，意味着该示例是典型的数据库的代表。 它不包括每一项功能的 SQL Server。 数据库设计遵循一组通用的标准，但有一个可能生成数据库的多种方法。

**最新版本**: [wide world 导入程序版本](http://go.microsoft.com/fwlink/?LinkID=800630)

**源的示例代码**: [wide world importers 计划](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers)。

**反馈**： 请将发送到[ sqlserversamples@microsoft.com ](mailto:sqlserversamples@microsoft.com)。

此示例的文档的组织方式如下：

## <a name="overview"></a>概述

示例公司 Wide World Importers，概述和示例通过寻址的工作流。

## <a name="main-oltp-database-wideworldimporters"></a>主 OLTP 数据库 WideWorldImporters

有关安装和配置核心说明数据库用于事务处理 (OLTP 的联机事务处理) 和运行分析 (HTAP-混合事务/分析处理) 的 WideWorldImporters。

架构和表 WideWorldImporters 数据库中使用的说明。  

描述如何 WideWorldImporters 利用核心 SQL Server 功能。

WideWorldImporters 数据库的示例查询。

## <a name="data-warehousing-and-analytics-database-wideworldimportersdw"></a>数据仓库和分析数据库 WideWorldImportersDW

有关安装和配置 OLAP 数据库 WideWorldImportersDW。

架构和表 WideWorldImportersDW 数据库，这是数据仓库和分析处理 (OLAP) 的示例数据库中使用的说明。

将数据从事务的数据库 WideWorldImporters 迁移到数据仓库 WideWorldImportersDW ETL （提取、 转换、 加载） 过程的工作流。

描述如何 WideWorldImportersDW 利用的分析处理 SQL Server 功能。

利用 WideWorldImportersDW 数据库示例分析查询。

## <a name="data-generation"></a>数据生成

描述如何附加数据可在示例数据库中，例如将插入销售生成并购买截至当前日期的数据。
