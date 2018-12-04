---
title: DQS 安全性 | Microsoft Docs
ms.custom: ''
ms.date: 10/01/2012
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 921927f5-1b1e-452a-a79e-c691829fd826
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 91b7f5cd25601dff60705465fadbb80a1b169dca
ms.sourcegitcommit: c19696d3d67161ce78aaa5340964da3256bf602d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/29/2018
ms.locfileid: "52616467"
---
# <a name="dqs-security"></a>DQS 安全性

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 安全基础结构基于 SQL Server 安全基础结构。 数据库管理员通过将用户与 DQS 角色相关联，向用户授予一组权限。 这样，可以确定用户可访问的 DQS 资源以及允许用户执行的功能活动。  
  
## <a name="dqs-roles"></a>DQS 角色  
 有四种 DQS 角色。 一种角色是数据库管理员 (DBA)，主要负责处理产品安装、数据库维护和用户管理等工作。 该角色主要使用 SQL Server Management Studio，而不是 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 应用程序。 他们的服务器角色是 sysadmin。  
  
 其他三个角色是信息工作者，即通过在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 应用程序中工作直接使用产品的数据专员。 这些角色包括：  
  
-   DQS 管理员  （dqs_administrator 角色）可以在产品范围内执行任何操作。 该管理员可以编辑和执行项目、创建和编辑知识库、终止活动、停止活动中的过程，可以更改配置和 Reference Data Services 设置。 但是，DQS 管理员无法安装服务器或添加新用户。 必须由数据库管理员执行这些操作。  
  
-   **DQS KB 编辑人员** （dqs_kb_editor 角色）可以执行所有 DQS 活动，但管理除外。 KB 编辑人员可以编辑和执行项目，以及创建和编辑知识库。 他们可以查看活动监视数据，但不能终止或停止活动或履行管理职责。  
  
-   **DQS KB 操作员** （dqs_kb_operator 角色）可以编辑和执行项目。 他们不能执行任何形式的知识管理；也不能创建或更改知识库。 他们可以查看活动监视数据，但不能终止活动或履行管理职责。  
  
## <a name="user-management"></a>用户管理  
 数据库管理员 (DBA) 可以创建 DQS 用户，并将用户与 SQL Server Management Studio 中的 DQS 角色相关联。 DBA 通过将 SQL 登录名添加为 DQS_MAIN 数据库的用户，并将每个用户与其中一个 DQS 角色相关联，以管理其权限。 每个角色都会被授予针对 DQS_MAIN 数据库的一组存储过程的权限。 这三个 DQS 角色不适用于 DQS_PROJECTS 和 DQS_STAGING_DATA 数据库。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|任务说明|主题|  
|----------------------|-----------|  
|介绍如何使用 SQL Server Management Studio 创建用户并授予 DQS 角色。|[在 SSMS 中管理 DQS 用户](https://msdn.microsoft.com/library/955af01d-00da-4c51-9311-f3848749df54)|  
  
  
