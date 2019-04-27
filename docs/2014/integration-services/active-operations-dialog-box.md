---
title: 活动操作对话框 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.ssms.isoperations.executions.f1
- sql12.ssis.ssms.isoperations.general.f1
ms.assetid: 5bb0fcd6-0ce9-488a-85b8-25dddaa03cda
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: efb8341b4e7124e244b5994aa2f83c664348b865
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62772302"
---
# <a name="active-operations-dialog-box"></a>“活动操作”对话框
  使用 **“活动操作”** 对话框可以查看 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务器上当前运行的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 操作的状态，例如部署、验证和包执行。 此数据存储在 SSISDB 目录中。  
  
 有关相关 [!INCLUDE[tsql](../includes/tsql-md.md)] 视图的详细信息，请参阅 [catalog.operations（SSISDB 数据库）](/sql/integration-services/system-views/catalog-operations-ssisdb-database)、[catalog.validations（SSISDB 数据库）](/sql/integration-services/system-views/catalog-validations-ssisdb-database)和 [catalog.executions（SSISDB 数据库）](/sql/integration-services/system-views/catalog-executions-ssisdb-database)  
  
 **您希望做什么？**  
  
1.  [打开“活动操作”对话框](#open_dialog)  
  
2.  [配置选项](#options)  
  
##  <a name="open_dialog"></a> 打开“活动操作”对话框  
  
1.  打开 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]。  
  
2.  连接 Microsoft SQL Server 数据库引擎  
  
3.  在对象资源管理器中，展开 **Integration Services** 节点，右键单击 **SSISDB**，然后单击 **“活动操作”**。  
  
##  <a name="options"></a> 配置选项  
  
### <a name="options"></a>选项  
 **类型**  
 指定操作的类型。 以下是可能的值为**类型**字段与 TRANSACT-SQL 的 operations_type 列中的对应值`catalog.operations`视图。  
  
|||  
|-|-|  
|Integration Services 初始化|1|  
|操作清除（SQL 代理作业）|2|  
|项目版本清除（SQL 代理作业）|3|  
|部署项目|101|  
|还原项目|106|  
|创建和启动包执行|200|  
|停止操作（停止验证或执行）|202|  
|验证项目|300|  
|验证包|301|  
|配置目录|1000|  
  
 **停止**  
 单击以停止当前正在运行的操作。  
  
  
