---
title: 选项 （查询结果-SQL 服务器多服务器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.sqleditors.multiserverresultssettings
- VS.ToolsOptionsPages.QueryResults.SqlServer.SQLMultiServerResults
ms.assetid: d6768bd8-9cb5-4606-a726-a33a1df9e1bb
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 6019a328463d27b4495ae0db70e844eb4e05d747
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66089969"
---
# <a name="options-query-results-sql-server-multi-server"></a>选项（“查询结果”-“SQL Server”-“多服务器”）
  在同时查询多个服务器时，可使用此页指定显示结果集的选项。 “合并结果”可将所有服务器中的结果集合并为单个结果集。 合并结果时，响应的第一个服务器将设置结果集的架构。 若要合并结果集，查询必须从每个服务器中返回具有相同列名的相同列数。 在合并结果时，如果某个服务器与第一个服务器在返回结果时返回的架构（列计数和列名称）不匹配，则会为该服务器显示一条消息。  
  
 如果不合并结果，每个服务器中的结果集将显示在其自己的网格中，并使用其自己的架构。  
  
## <a name="uielement-list"></a>UIElement 列表  
 **合并结果**  
 选中此复选框可将几个服务器组中的结果集合并到相同的网格中。  
  
 **将服务器名称添加到结果**  
 选中此复选框可包含一个额外的列，其中提供生成每一行的服务器的名称。  
  
 **将登录名添加到结果**  
 选中此复选框可包含一个额外的列，其中提供用于连接到提供每一行的服务器的登录名。  
  
## <a name="see-also"></a>请参阅  
 [创建中央管理服务器和服务器组&#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-a-central-management-server-and-server-group.md)   
 [同时对多个服务器执行语句 (SQL Server Management Studio)](../ssms/register-servers/execute-statements-against-multiple-servers-simultaneously.md)  
  
  
