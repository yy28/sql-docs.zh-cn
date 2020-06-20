---
title: 设置事务发布的分发保持期（SQL Server Management Studio） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- transaction retention periods [SQL Server replication]
- retention periods [SQL Server replication]
ms.assetid: 9a98c53a-fea5-4235-b23d-6c69587c5676
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a68f092c63e75196ab82a81d2a8ca36d13142813
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85055667"
---
# <a name="set-the-distribution-retention-period-for-transactional-publications-sql-server-management-studio"></a>设置事务发布的分发保持期 (SQL Server Management Studio)
  在 "**分发数据库属性- \<DistributionDatabase> ** " 对话框中指定最小分发保持期和最大分发保持期。 可从 "**分发服务器属性 \<Distributor> -** 对话框的"**常规**"页中获取此功能。 有关访问此对话框的详细信息，请参阅[查看和修改分发服务器和发布服务器属性](view-and-modify-distributor-and-publisher-properties.md)。  
  
### <a name="to-specify-the-distribution-retention-period"></a>指定分发保持期  
  
1.  在 "**分发服务器属性- \<Distributor> ** " 对话框的 "**常规**" 页上，单击分发数据库的属性按钮（**...**）。  
  
2.  若要指定最小分发保持期，请在 **“至少”** 框中输入一个值；若要指定最大分发保持期，请在 **“但不超过”** 框中输入一个值。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [配置分发](configure-distribution.md)   
 [订阅过期和停用](subscription-expiration-and-deactivation.md)  
  
  
