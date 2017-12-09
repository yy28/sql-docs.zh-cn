---
title: "使用 Azure SQL 数据库中的 R |Microsoft 文档"
ms.custom: 
ms.date: 12/04/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0a90c438-d78b-47be-ac05-479de64378b2
caps.latest.revision: "1"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: ef6573ca1d682ae4b4f4336ad6f809f1e094e9fc
ms.sourcegitcommit: 16347f3f5ed110b5ce4cc47e6ac52b880eba9f5f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="using-r-in-azure-sql-database"></a>在 Azure SQL Database 中使用 R

自 2017 年 10 月，就是在 SQL Server 开发团队宣布计划来支持的 R 代码数据库中使用类似于 SQL Server 2016 中的 R Services 的存储的过程的执行。 此功能是仍在开发。

若要保持最新公开发布的版本计划和即将到来的事件，请参阅[SQL Server 博客](https://blogs.technet.microsoft.com/dataplatforminsider/)或[Microsoft R Server 博客](https://blogs.msdn.microsoft.com/rserver/)。

> [!IMPORTANT]
> 已宣布的初始预览版本已适用于测试和仅浏览。 目前，仅，有限的区域中的 Azure SQL 数据库中提供了功能; 功能将比较 SQL Server 2016 或 2017年中支持的功能受到限制。

**Azure 资源**

在此期间，我们建议你使用在 Azure 应用商店都可用的 SQL Server 2017 虚拟机之一： 

+ [设置用于在 Azure 上的机器学习的虚拟机](provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md)

同时查看这些 Vm，但这与各种受欢迎的机器学习工具都被预配置：

+ [数据科学虚拟机](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/overview)
+ [深入学习虚拟机](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/deep-learning-dsvm-overview)， 

