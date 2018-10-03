---
title: 删除根据保留的 GEOMETRY 和 GEOGRAPHY 数据类型命名的 Udt |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- geometry data type [SQL Server], UDTs
- geography data type [SQL Server], UDTs
ms.assetid: a167ce3a-50b4-4e77-a884-adb23b586c72
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f93b179da229793c65db452e4f38bb1f08fbfad1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48135247"
---
# <a name="remove-udts-named-after-the-reserved-geometry-and-geography-data-types"></a>删除根据保留的 GEOMETRY 和 GEOGRAPHY 数据类型命名的 UDT
  升级顾问检测到根据为 `geometry` 或 `geography` 数据类型保留的术语命名的用户定义类型 (UDT)。 `geometry` 和 `geography` 数据类型是空间数据功能的一部分。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 用于空间数据类型的术语不应用作公共语言运行时 (CLR) 或别名 UDT 的名称。  
  
## <a name="corrective-action"></a>纠正措施  
 删除根据数据类型命名的 UDT，并使用非保留名称重新创建 UDT。  
  
## <a name="external-resources"></a>外部资源  
 [创建用户定义类型](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
 [空间数据类型概述](../../relational-databases/spatial/spatial-data-types-overview.md)  
  
  
