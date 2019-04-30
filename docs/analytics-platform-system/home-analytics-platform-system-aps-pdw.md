---
title: Analytics Platform System 文档 | Microsoft Docs
description: Microsoft Analytics Platform System (APS) 是一种设计用于数据仓库和大数据分析的数据平台，它可为端到端商业智能解决方案提供深度数据集成、高速查询处理、高度可伸缩存储，以及简单维护。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/18/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: bc8765d0bc8fe4b5b9ab3b4bcc98ce940f99400c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63181732"
---
# <a name="microsoft-analytics-platform-system"></a>Microsoft Analytics Platform System

Microsoft Analytics Platform System (APS) 是一种设计用于数据仓库和大数据分析的数据平台，它可为端到端商业智能解决方案提供深度数据集成、高速查询处理、高度可伸缩存储，以及简单维护。

![设备体系结构](media/architecture-high-level.png "设备体系结构")

Analytics Platform System 承载的 SQL Server 并行数据仓库 (PDW) 是运行大规模并行处理 (MPP) 数据仓库的软件。

PolyBase 技术将关系 PDW 数据与来自多个源（包括 Hortonworks on Windows Server、Hortonworks on Linux、Cloudera on Linux、HDInsight 的 Windows Azure Blob 存储）的 Hadoop 数据结合在一起。 这些高级数据集成功能，加上与商业智能工具的深度集成，让 Analytics Platform System 能够返回集成分析，使业务决策人能够做出更好、有更深入见解的业务决策。

Analytics Platform System 可作为预安装和预配了硬件和软件的设备发送到你的数据中心，以运行多个工作负荷。 购买 Analytics Platform System 时，会根据业务需求为 PDW 购买计算节点。

Analytics Platform System 不仅运行速度块，而且可缩放，其采用高冗余和高可用性设计，是值得用户信赖的用于处理最关键业务数据的可靠平台。 Analytics Platform System 设计简单，易于学习和管理。 用于分析 Hadoop 数据的 PDW PolyBase 技术与商业智能工具的深度集成，使其成为构建端到端解决方案的综合平台。

## <a name="parallel-data-warehouse-software-designed-for-massively-parallel-processing"></a>并行数据仓库是设计用于大规模并行处理的软件

使用 PDW 作为端到端商业智能解决方案的核心关系数据仓库组件。 利用 PDW 的大规模并行处理 (MPP) 设计进行查询，通常比基于对称多处理 (SMP) 数据库管理系统的传统数据仓库要快 50 倍。

> [!NOTE]
> 快 50 倍意味着完成查询只需几分钟，而不是几小时，或者只需几秒钟，而不是几分钟。 此项突破性性能让业务分析师更快地生成更多结果，并且能够轻松执行即席查询或深入研究细节。 这样，企业就可以做出更好、更快的决策。

除了实现突破性的查询性能外，PDW 还易于：

- 增长到任何位置的数据仓库从几兆兆字节到单个设备，通过将"缩放单位"添加到现有系统中的数据超过 6 拍字节。

- 信任你的数据会在那里时需要由于内置高冗余和高可用性。

- 解决加载和合并数据的现代数据挑战。

- 通过使用 PDW 的高度并行化的 PolyBase 技术将 Hadoop 数据集成以快速分析关系数据。

- 使用商业智能工具构建全面的端到端解决方案。

## <a name="next-steps"></a>后续步骤

有关 PDW 优势的更多信息，请参阅 MSDN 上的白皮书 [A Breakthrough Platform for Next-Generation Data Warehousing and Big Data Solutions](https://docs.microsoft.com/previous-versions/sql/sql-server-2012/dn520808%28v=msdn.10%29)（下一代数据仓库和大数据解决方案的突破性平台）。
