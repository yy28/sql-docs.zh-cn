---
description: 组织作业
title: 组织作业
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- job category
- organize jobs
ms.assetid: 629c3e06-f933-483b-8621-280dbb7a7bd1
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: ad737fea7ae2a9c55977ffb9d838fdcbeccad412
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88319043"
---
# <a name="organize-jobs"></a>组织作业
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> [Azure SQL 托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支持大多数（但不是所有）SQL Server 代理功能。 有关详细信息，请参阅 [Azure SQL 托管实例与 SQL Server 的 T-SQL 区别](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

作业类别有助于您组织作业，从而更容易筛选和分组。 例如，可以将所有数据库备份作业组织到“数据库维护”类别中。 此外，还可以创建自己的作业类别。  
  
> [!WARNING]  
> 多服务器类别仅存在于主服务器上。 主服务器上仅提供了一个默认作业类别：“[未分类(多服务器)]”****。 下载多服务器作业后，其类别将在目标服务器上更改为“来自 MSX 的作业” **** 。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|说明|主题|  
|-|-|  
|介绍如何创建作业类别。|[创建作业类别](../../ssms/agent/create-a-job-category.md)|  
|介绍如何删除作业类别。|[删除作业类别](../../ssms/agent/delete-a-job-category.md)|  
|介绍如何向作业类别分配一个作业。|[将作业分配到作业类别](../../ssms/agent/assign-a-job-to-a-job-category.md)|  
|介绍如何更改作业类别的成员身份。|[更改作业类别的成员身份](../../ssms/agent/change-the-membership-of-a-job-category.md)|  
|介绍如何列出类别信息。|[列出作业类别信息](../../ssms/agent/list-job-category-information.md)|  
  
