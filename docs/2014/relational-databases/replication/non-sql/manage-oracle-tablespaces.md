---
title: 管理 Oracle 表空间 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], managing tablespaces
- tablespaces [SQL Server replication]
ms.assetid: b8ea6c3b-01d6-4efc-bbfb-03b264530bbd
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a3624aed38a7a5bf75e0c0807aa8d3657156264f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85068594"
---
# <a name="manage-oracle-tablespaces"></a>管理 Oracle 表空间
  表空间是一个数据库存储单元，大致相当于 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的文件组。 表空间允许存储和管理各个组内的数据库对象。 有关详细信息，请参阅 Oracle 文档。  
  
 如果将表配置为 Oracle 发布的一部分，则可以选择指定在存储复制记录信息时使用现有的 Oracle 表空间。 如果未指定，则复制对象的表空间就是与配置发布服务器时配置的复制管理用户架构相关联的默认表空间。  
  
 **为项目记录表指定表空间**：  
  
-   在 **“项目属性”** 对话框中指定表空间。 有关访问此对话框的详细信息，请参阅 [View and Modify Publication Properties](../publish/view-and-modify-publication-properties.md)。  
  
-   使用 [sp_changearticle (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-changearticle-transact-sql)。 若要使用 **sp_changearticle**，请指定下列内容：  
  
    -   参数的 Oracle 发布服务器的名称 **@publisher** 。  
  
    -   参数的 Oracle 发布的名称 **@publication** 。  
  
    -   参数的项目名称 **@article** 。  
  
    -   参数的 "表空间" 的值 **@property** 。  
  
    -   参数表空间的名称 **@value** 。  
  
## <a name="see-also"></a>另请参阅  
 [配置 Oracle 发布服务器](configure-an-oracle-publisher.md)   
 [在 Oracle 发布服务器上创建的对象](objects-created-on-the-oracle-publisher.md)  
  
  
