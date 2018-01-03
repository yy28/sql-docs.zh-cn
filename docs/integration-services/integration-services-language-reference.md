---
title: "Integration Services 语言参考 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
ms.assetid: c67b72f1-0a1e-42f0-878a-84e85efc915b
caps.latest.revision: "7"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a20bca3837b6bcf34bed571b59ee493eab72122f
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="integration-services-language-reference"></a>Integration Services 语言参考
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  本节介绍用于管理已部署到 [!INCLUDE[tsql](../includes/tsql-md.md)] 实例的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] API。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 在称为 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 目录的数据库中存储对象、设置和操作数据。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 目录的默认名称为 SSISDB。 目录中存储的对象包括项目、包、参数环境和操作历史记录。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 目录将其数据存储在用户看不到的内部表中。 不过，它通过您可以查询的一组公共视图公开您所需的信息。 它还提供了一组存储过程，您可用来对目录执行常见任务。  
  
 通常，您可以通过打开 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 来管理目录中的 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 对象。 但是，您还可以直接使用数据库视图和存储过程，或者编写用于调用托管 API 的自定义代码。 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 和托管 API 查询这些视图，并调用本节中介绍的存储过程来执行许多任务。  
  
## <a name="in-this-section"></a>本节内容  
 [视图（Integration Services 目录）](../integration-services/system-views/views-integration-services-catalog.md)  
 查询视图以检查 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 对象、设置和操作数据。  
  
 [存储过程（Integration Services 目录）](../integration-services/system-stored-procedures/stored-procedures-integration-services-catalog.md)  
 调用存储过程以添加、删除或修改 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 对象和设置。  
  
 [函数（Integration Services 目录）](http://msdn.microsoft.com/library/9f2aec85-3d4c-415f-b1f8-8328a60b1c7f)  
 调用函数以管理 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
  
