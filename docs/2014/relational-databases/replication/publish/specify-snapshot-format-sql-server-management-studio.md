---
title: 指定快照格式 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], formats
- snapshot replication [SQL Server], formats
ms.assetid: 7c95f545-731a-4743-9acb-0b325ef9b98b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8e13b0635e750f8b6e59420fd25fe81af74eb7a0
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52811039"
---
# <a name="specify-snapshot-format-sql-server-management-studio"></a>指定快照格式 (SQL Server Management Studio)
  在“发布属性 - \<发布>”对话框的“快照”页上指定快照格式。 有关访问此对话框的详细信息，请参阅 [View and Modify Publication Properties](view-and-modify-publication-properties.md)。  
  
### <a name="to-specify-snapshot-format"></a>指定快照格式  
  
1.  在“发布属性 - \<发布>”对话框的“快照”页上，选择“本机 SQL Server - 所有订阅服务器都必须是运行 SQL Server 的服务器”或“字符 - 如果发布服务器或订阅服务器没有运行 SQL Server，则需要此项”。  
  
    > [!NOTE]  
    >  建议选择本机格式，除非此发布必须支持对 [!INCLUDE[ssEW](../../../includes/ssew-md.md)] 数据库或非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库的订阅。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [配置快照属性（复制 Transact-SQL 编程）](configure-snapshot-properties-replication-transact-sql-programming.md)   
 [更改发布和项目属性](change-publication-and-article-properties.md)   
 [使用快照初始化订阅](../initialize-a-subscription-with-a-snapshot.md)  
  
  
