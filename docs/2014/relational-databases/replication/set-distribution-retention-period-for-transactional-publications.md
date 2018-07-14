---
title: 分发保持期设置为事务发布 (SQL Server Management Studio) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- transaction retention periods [SQL Server replication]
- retention periods [SQL Server replication]
ms.assetid: 9a98c53a-fea5-4235-b23d-6c69587c5676
caps.latest.revision: 35
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0c2997c2d3c07fad951bf750e852e9e4ab37e9da
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37225303"
---
# <a name="set-the-distribution-retention-period-for-transactional-publications-sql-server-management-studio"></a>设置事务发布的分发保持期 (SQL Server Management Studio)
  在“分发数据库属性 - \<分发数据库>”对话框中指定最小分发保持期和最大分发保持期。 可以从“分发服务器属性 - \<分发服务器>”对话框的“常规”页中访问该对话框。 有关访问此对话框的详细信息，请参阅[查看和修改分发服务器和发布服务器属性](view-and-modify-distributor-and-publisher-properties.md)。  
  
### <a name="to-specify-the-distribution-retention-period"></a>指定分发保持期  
  
1.  在“分发服务器属性 - \<分发服务器>”对话框的“常规”页上，单击分发数据库的属性按钮 (**…**)。  
  
2.  若要指定最小分发保持期，请在 **“至少”** 框中输入一个值；若要指定最大分发保持期，请在 **“但不超过”** 框中输入一个值。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [“配置分发”](configure-distribution.md)   
 [订阅过期和停用](subscription-expiration-and-deactivation.md)  
  
  
