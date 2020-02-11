---
title: SQLXML 托管类 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- .NET Framework [SQLXML], Managed Classes
- SQL Server .NET Data Provider
- Managed Classes [SQLXML], about managed classes
- providers [SQLXML], SQL Server .NET Data Provider
- data providers [SQLXML], SQL Server .NET Data Provider
- Managed Classes [SQLXML]
- XML [SQLXML]
- SQLXML Managed Classes
- providers [SQLXML], SQLXML Managed Classes
- data providers [SQLXML], SQLXML Managed Classes
- SQLXML, Managed Classes
ms.assetid: 73a5faeb-dabf-4895-acb5-a9651b646065
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 677d769f54dab338e65b171bed50b6abb69e356a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66010789"
---
# <a name="sqlxml-managed-classes"></a>SQLXML 托管类
  
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 托管类在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 中公开 SQLXML 4.0 的功能。 利用 SQLXML 托管类，您可以编写 C# 应用程序，以便访问 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例中的 XML 数据，将该数据载入 .NET Framework 环境并进行处理，然后将更新作为 DiffGram 发回 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以应用此更新。 使用 SQLXML 托管类向 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库应用更新时必须使用映射架构。 有关工作示例，请参阅[在 .Net 环境中访问 SQLXML 功能](accessing-sqlxml-functionality-in-the-net-environment.md)。  
  
 若要配合使用 SQLXML 托管类和 SQLXML 4.0，必须安装 Microsoft Visual Studio。  
  
> [!NOTE]  
>  .NET Framework 包括 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .NET 数据访问接口。 该访问接口可用于从 .NET 环境访问 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]；但是，它只能处理传统 SQL 查询（即除 FOR XML 查询以外的关系数据库查询）。 您不能在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中执行 XML 模板或服务器端 XPath 查询。  
  
## <a name="in-this-section"></a>本节内容  
 [SQLXML 托管类对象模型](../../../database-engine/dev-guide/sqlxml-managed-classes-object-model.md)  
 记录 SQLXML 托管类及其属性和方法。  
  
 [使用 SQLXML 托管类](sqlxml-4-0-net-framework-support-managed-classes.md)  
 提供使用 SQLXML 托管类的示例。  
  
  
