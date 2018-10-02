---
title: 为复制启用数据库 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server replication]
ms.assetid: 8092faa3-9cff-4f81-926c-6a0070d1ce2c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ce3bc10ad615e449da26e55d64b05ca36b6d10ca
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47729505"
---
# <a name="enable-a-database-for-replication-sql-server-management-studio"></a>为复制启用数据库 (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  当 **sysadmin** 固定服务器角色的成员使用新建发布向导创建发布时，将为复制隐式启用数据库。 **sysadmin** 固定服务器角色的成员还可以为复制显式启用数据库，使 **db_owner** 固定数据库角色的成员可以在该数据库中创建一个或多个发布。 若要显式启用数据库，请使用“发布服务器属性 - \<发布服务器>”对话框的“发布数据库”页。 有关访问此对话框的详细信息，请参阅 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)。  
  
### <a name="to-enable-a-database-for-replication"></a>为复制启用数据库  
  
1.  在“发布服务器属性 - \<发布服务器>”对话框的“发布数据库”页上，选择每个要复制的数据库所对应的“事务”和/或“合并”复选框。 选择 **“事务”** 将为快照复制启用数据库。  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
  
