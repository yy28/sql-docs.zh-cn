---
title: 删除 UDT&#39;保留的 ORDPATH 数据类型名为 s |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 474e910a-6abb-4e28-acc2-055338c011d4
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b98fa9765a40d3eb9c05852e9c20c05c4bb818a0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62856313"
---
# <a name="remove-udt39s-named-after-the-reserved-ordpath-data-type"></a>删除 UDT&#39;s 名为保留的 ORDPATH 数据类型
  升级顾问检测到根据为 `ORDPATH` 数据类型保留的术语命名的用户定义类型 (UDT)。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 用于内置数据类型的术语不应用作公共语言运行时 (CLR) 或别名 UDT 的名称。  
  
## <a name="corrective-action"></a>纠正措施  
 删除根据数据类型命名的 UDT，并使用非保留名称重新创建 UDT。  
  
## <a name="external-resources"></a>外部资源  
 [创建用户定义类型](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
  
