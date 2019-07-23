---
title: 在企业中优化自动化管理 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- performance [SQL Server], automated administration
- tuning automated administration [SQL Server]
- monitoring performance [SQL Server], automated administration
ms.assetid: 671fed35-3859-4b0d-8f38-4dd07436857e
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 4cbe403081080e9550052644c2b1e25d6455ce9b
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2019
ms.locfileid: "68261114"
---
# <a name="tune-automated-administration-across-an-enterprise"></a>在企业中优化自动化管理
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL 数据库托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支持大多数但并非所有 SQL Server 代理功能。 有关详细信息，请参阅 [Azure SQL 数据库托管实例与 SQL Server 之间的 T-SQL 差异](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

使用 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的多服务器管理利用了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的自我优化功能。 因此，在正常情况下，不需要额外进行作业优化。 但当您运行作业、生成警报和通知操作员时，网络负荷会相应增加。 您可以优化企业中的自动化管理以尽量减少这些活动导致的网络通信流量。  
  
## <a name="see-also"></a>另请参阅  
[监视数据流引擎的性能](../../integration-services/performance/performance-counters.md)  
  
