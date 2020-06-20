---
title: 为复制启用数据库 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server replication]
ms.assetid: 8092faa3-9cff-4f81-926c-6a0070d1ce2c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 307d52e24187e35c1c30f609facd13bfad569216
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85010739"
---
# <a name="enable-a-database-for-replication-sql-server-management-studio"></a>为复制启用数据库 (SQL Server Management Studio)
  当 **sysadmin** 固定服务器角色的成员使用新建发布向导创建发布时，将为复制隐式启用数据库。 **sysadmin** 固定服务器角色的成员还可以为复制显式启用数据库，使 **db_owner** 固定数据库角色的成员可以在该数据库中创建一个或多个发布。 若要显式启用数据库，请使用 "**发布服务器属性- \<Publisher> ** " 对话框的 "**发布数据库**" 页。 有关访问此对话框的详细信息，请参阅 [Create a Publication](publish/create-a-publication.md)。  
  
### <a name="to-enable-a-database-for-replication"></a>为复制启用数据库  
  
1.  在 " ** \<Publisher> 发布服务器属性-** " 对话框的 "**发布数据库**" 页上，选中要复制的每个数据库的 "**事务**" 和/或 "**合并**" 复选框。 选择 **“事务”** 将为快照复制启用数据库。  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
  
