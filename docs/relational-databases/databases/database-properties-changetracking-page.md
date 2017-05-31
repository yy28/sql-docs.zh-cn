---
title: "数据库属性（“更改跟踪”页）| Microsoft Docs"
ms.custom: 
ms.date: 01/07/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.databaseproperties.changetracking.f1
ms.assetid: 9b929640-bc62-449b-9b06-b5a77b8cf372
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2aab898a267244d585d1d09bc66eaca4814895a1
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="database-properties-changetracking-page"></a>数据库属性（“更改跟踪”页）
  使用此页可查看或修改所选数据库的更改跟踪设置。 有关在此页上可用选项的详细信息，请参阅[启用和禁用更改跟踪 (SQL Server)](../../relational-databases/track-changes/enable-and-disable-change-tracking-sql-server.md)。  
  
## <a name="options"></a>选项  
 **更改跟踪**  
 用于启用或禁用数据库的更改跟踪。  
  
 若要启用更改跟踪，您必须拥有修改数据库的权限。  
  
 将其值设置为 **True** 即可设置允许对各个表启用更改跟踪的数据库选项。  
  
 还可以使用 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md)来配置更改跟踪。  
  
 **保持期**  
 指定在数据库中保留更改跟踪信息的最短期限。 只有当“自动清除”的值为 **True** 时，才会删除数据。  
  
 默认值为 2。  
  
 **保持期单位**  
 指定“保持期”值的单位。 可以选择 **“天”**、 **“小时”**或 **“分钟”**。 默认值为 **“天”**。  
  
 最短保持期为 1 分钟。 不存在最长保持期。  
  
 **自动清除**  
 指示是否在经过指定的保持期后自动删除更改跟踪信息。  
  
 启用“自动清除”会将任何先前自定义的保持期重置为默认保持期（即 2 天）。  
  
## <a name="see-also"></a>另请参阅  
 [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE (SQL Server Transact-SQL)](../../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
  

