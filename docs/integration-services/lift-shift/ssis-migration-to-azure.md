---
title: SQL Server Integration Services 到 Azure 的迁移概述 | Microsoft Docs
description: 本文重点介绍将 SQL Server Integration Services 迁移到 Azure 的过程和工具。
ms.date: 04/10/2020
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 81fb9b9cb792cf350137a375e7a2e25643656b6e
ms.sourcegitcommit: 335d27d0493ddf4ffb770e13f8fe8802208d25ae
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2020
ms.locfileid: "81002848"
---
# <a name="migrate-on-premises-ssis-workloads-to-ssis-in-adf"></a>将本地 SSIS 工作负载迁移到 ADF 中的 SSIS

本文列出了可帮助将 SQL Server Integration Services (SSIS) 工作负载迁移到 ADF 中的 SSIS 的过程和工具。

[迁移概述](https://docs.microsoft.com/azure/data-factory/scenario-ssis-migration-overview)重点介绍了 ETL 工作负载从本地 SSIS 到 ADF 中的 SSIS 的总体迁移过程。

迁移过程包括以下两个阶段：[评估](https://docs.microsoft.com/azure/data-factory/scenario-ssis-migration-overview#assessment)和[迁移](https://docs.microsoft.com/azure/data-factory/scenario-ssis-migration-overview#migration)。

## <a name="assessment"></a>评估

数据迁移助手 (DMA) 是出于此目的一个免费下载的工具，可在本地安装和执行。 可以创建 Integration Services 类型的 DMA 评估项目，以批处理评估 SSIS 包并识别兼容性问题。

获取[数据迁移助手](https://docs.microsoft.com/sql/dma/dma-overview)并[执行包评估](https://docs.microsoft.com/sql/dma/dma-assess-ssis)。

## <a name="migration"></a>迁移

根据源 SSIS 包的存储类型和数据库工作负载的迁移目标，迁移 SSIS 包和计划 SSIS 包执行的 SQL Server 代理作业的步骤可能会有所不同。 有关详细信息，请参阅 [本页](https://docs.microsoft.com/azure/data-factory/scenario-ssis-migration-overview#migration)。

## <a name="next-steps"></a>后续步骤

- [将 SSIS 包迁移到 Azure SQL 数据库托管实例](https://docs.microsoft.com/azure/dms/how-to-migrate-ssis-packages-managed-instance)。
- [使用 SQL Server Management Studio (SSMS) 将 SSIS 作业迁移到 Azure 数据工厂 (ADF)](https://docs.microsoft.com/azure/data-factory/how-to-migrate-ssis-job-ssms)。
