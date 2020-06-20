---
title: 删除以保留的 GEOMETRY 和 GEOGRAPHY 数据类型命名的 Udt |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- geometry data type [SQL Server], UDTs
- geography data type [SQL Server], UDTs
ms.assetid: a167ce3a-50b4-4e77-a884-adb23b586c72
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 4977d45d53e1114edc8e04ad504963bae0b9eb9d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059115"
---
# <a name="remove-udts-named-after-the-reserved-geometry-and-geography-data-types"></a>删除根据保留的 GEOMETRY 和 GEOGRAPHY 数据类型命名的 UDT
  升级顾问检测到根据为 `geometry` 或 `geography` 数据类型保留的术语命名的用户定义类型 (UDT)。 `geometry` 和 `geography` 数据类型是空间数据功能的一部分。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>说明  
 用于空间数据类型的术语不应用作公共语言运行时 (CLR) 或别名 UDT 的名称。  
  
## <a name="corrective-action"></a>纠正措施  
 删除根据数据类型命名的 UDT，并使用非保留名称重新创建 UDT。  
  
## <a name="external-resources"></a>外部资源  
 [Creating a User-Defined Type（创建用户定义类型）](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
 [空间数据类型概述](../../relational-databases/spatial/spatial-data-types-overview.md)  
  
  
