---
title: "设置事务发布的分发保持期 (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "事务保持期 [SQL Server 复制]"
  - "保持期 [SQL Server 复制]"
ms.assetid: 9a98c53a-fea5-4235-b23d-6c69587c5676
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 设置事务发布的分发保持期 (SQL Server Management Studio)
  指定的最小分发保持期和最大分发保持期 **分发数据库属性-\< 分发数据库>** 对话框。 这是可从 **常规** 页 **分发服务器属性-\< 分发服务器>** 对话框。 有关访问此对话框中的详细信息，请参阅 [查看和修改分发服务器和发布服务器属性](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)。  
  
### 指定分发保持期  
  
1.  在 **常规** 页 **分发服务器属性-\< 分发服务器>** 对话框框中，单击属性按钮 (**...**) 分发数据库。  
  
2.  若要指定最小分发保持期，请在 **“至少”** 框中输入一个值；若要指定最大分发保持期，请在 **“但不超过”** 框中输入一个值。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## 另请参阅  
 [配置分发](../../relational-databases/replication/configure-distribution.md)   
 [订阅过期和停用](../../relational-databases/replication/subscription-expiration-and-deactivation.md)  
  
  