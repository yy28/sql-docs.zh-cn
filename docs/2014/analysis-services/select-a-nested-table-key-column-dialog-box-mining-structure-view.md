---
title: "\"选择嵌套表键列\" 对话框（\"挖掘结构\" 视图） |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.structure.addnestedtable.f1
helpviewer_keywords:
- Select a Nested Table Key Column dialog box
ms.assetid: f68b89a7-17df-45f8-ba7f-b458cd9b1ec3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8edfea95968bee0dc1103f8069ecfe9e0d08e3ed
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66069764"
---
# <a name="select-a-nested-table-key-column-dialog-box-mining-structure-view"></a>“选择嵌套表键列”对话框（“挖掘结构”视图）
  可以使用 **“选择嵌套表键列”** 对话框，指定将用作新嵌套表的键的列。 在您退出此对话框后，挖掘结构中将添加一个包含指定键列的新表。 通过右键单击结构，再选择“添加列”，可以向嵌套表中添加其他列。**** 根据使用的是 OLAP 挖掘模型还是关系挖掘模型，该对话框将包含不同的选项。  
  
## <a name="options"></a>选项  
 **源表**  
 挖掘模型所基于的表。  
  
 此选项仅用于关系挖掘模型。  
  
 **源列**  
 源表中所有可用作嵌套表键的列的列表。  
  
 此选项仅用于关系挖掘模型。  
  
 **显示列类型**  
 可用列数据类型的列表。 选中或清除数据类型可以对 **“源列”** 中列的列表进行筛选。 只有与所选数据类型匹配的列才会显示在 **“源列”** 列表中。  
  
 此选项仅用于关系挖掘模型。  
  
 **属性**  
 可用作嵌套表键的属性的列表。  
  
 此选项仅用于 OLAP 挖掘模型。  
  
## <a name="see-also"></a>另请参阅  
 [挖掘结构视图 &#40;数据挖掘模型设计器&#41;](mining-structure-view-data-mining-model-designer.md)  
  
  
