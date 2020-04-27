---
title: 服务器配置-排序规则 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- collation configuration, SQL Server
- collation configuration, Setup
- collation configuration
ms.assetid: e3986870-5be4-458b-b671-5ff12a27b022
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 521129056d4513af2f86fb7b70b26621cb881b80
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66092292"
---
# <a name="server-configuration---collation"></a>服务器配置 - 排序规则
  可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装向导的“服务器配置 – 排序规则”页上修改 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 排序时所用的排序规则设置。 选择相应选项以匹配其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装或者其他计算机的排序规则设置。  
  
## <a name="options"></a>选项  
 为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 进行自定义  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供了两组排序规则：Windows 排序规则和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 排序规则。 您可以为 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]指定不同的排序规则设置，也可以为它们指定相同的排序规则。  
  
 默认情况下，对于美国英语系统区域设置，选择的是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 排序规则。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 本地化版本的默认排序规则由您的计算机的 Windows 系统区域设置决定。  
  
 仅当此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装的排序规则设置必须与另一 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例所用的排序规则设置相匹配，或者必须与另一台计算机的 Windows 系统区域设置相匹配时，才应更改默认设置。  
  
 **注意** [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 仅使用 Windows 排序规则。 如果计划安装 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，请在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装期间，选择 Windows 排序规则，以确保 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]之间结果的一致性。  
  
 有关详细信息，请参阅 [Collation Settings in Setup](https://go.microsoft.com/fwlink/?LinkId=190977)（安装程序中的排序规则设置）。  
  
## <a name="best-practices"></a>最佳方案  
 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序使用的 Windows 系统区域设置以及相应的默认排序规则的表的详细信息，请参阅 [Collation Settings in Setup](https://go.microsoft.com/fwlink/?LinkId=190977)（安装程序中的排序规则设置）。  
  
 如果可能，请为您的组织使用一个排序规则。 这样就不必为每个数据库、列、表达式或标识符显式指定排序规则。 如果必须使用多个排序规则和代码页设置，请对查询进行编码，以考虑排序规则优先顺序规则。 有关详细信息，请参阅联机丛书主题中的[排序规则优先级 (Transact-SQL)](/sql/t-sql/statements/collation-precedence-transact-sql)。  
  
 为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 选择排序规则时，请考虑下列建议：  
  
-   如果基于二进制码位的排序顺序可接受，请选择 BINARY2 排序规则。  
  
-   选择 Windows 排序规则以便在各数据类型之间进行一致的比较。  
  
-   使用新的 100 级排序规则以便获得更好的语言排序支持。 有关详细信息，请参阅 [排序规则和 Unicode 支持](../../relational-databases/collations/collation-and-unicode-support.md)。  
  
-   如果您计划将数据库迁移到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的升级实例，则选择与您的数据库的现有排序规则匹配的排序规则。  
  
  
