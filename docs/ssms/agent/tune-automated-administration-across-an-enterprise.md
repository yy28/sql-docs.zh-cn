---
title: 在企业中优化自动化管理
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- performance [SQL Server], automated administration
- tuning automated administration [SQL Server]
- monitoring performance [SQL Server], automated administration
ms.assetid: 671fed35-3859-4b0d-8f38-4dd07436857e
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b43a1298c16ba1e51459852f8c775dd67b5b4a7b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85755029"
---
# <a name="tune-automated-administration-across-an-enterprise"></a>在企业中优化自动化管理

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> [Azure SQL 数据库托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支持大多数但并非所有 SQL Server 代理功能。 有关详细信息，请参阅 [Azure SQL 数据库托管实例与 SQL Server 之间的 T-SQL 差异](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

使用 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的多服务器管理利用了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的自我优化功能。 因此，在正常情况下，不需要额外进行作业优化。 但当您运行作业、生成警报和通知操作员时，网络负荷会相应增加。 您可以优化企业中的自动化管理以尽量减少这些活动导致的网络通信流量。  

## <a name="see-also"></a>另请参阅

[监视数据流引擎的性能](../../integration-services/performance/performance-counters.md)