---
title: 修改边缘约束 | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- alter edge constraints
- edge constraints [SQL Server]
- CONNECTION constraints
- edge constraints [Azure SQL Database]
- graph edge constraints
- SQL Graph
ms.assetid: ''
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e5b6a471156f0b1371c727ce96aac72f4f812dac
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47650245"
---
# <a name="modify-edge-constraints"></a>修改边缘约束
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx.md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

  可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 在 [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)] 中修改边缘约束。 可以通过更改边缘约束子句顺序或添加新子句来修改边界表的边缘约束。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [Security](#Security)  
  
-   使用以下工具修改边缘约束：  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 需要对表的 ALTER 权限。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL
 若要使用 Transact-SQL 修改边缘约束，必须首先删除现有的边缘约束，然后用新定义重新创建。 有关详细信息，请参阅[删除边缘约束](../../relational-databases/tables/delete-edge-constraint.md)和[创建边缘约束](../../relational-databases/tables/create-edge-constraints.md)。    
 
