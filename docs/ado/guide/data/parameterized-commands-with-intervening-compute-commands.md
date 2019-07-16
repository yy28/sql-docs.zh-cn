---
title: 参数化命令与中间 COMPUTE 命令 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], parameterized commands
- parameterized commands [ADO]
- APPEND clause [ADO]
- COMPUTE command [ADO]
ms.assetid: 732f624f-8900-4608-9815-194302d22e8b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fb6bc2b9f7e53caf28f44daf39815850940b9d3a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924727"
---
# <a name="parameterized-commands-with-intervening-compute-commands"></a>参数化命令与中间 COMPUTE 命令
典型的参数化的形状 APPEND 命令具有创建父级的子句**记录集**使用一个查询命令和创建子级的另一个子句**记录集**使用参数化的查询命令-即，包含参数占位符的命令 (一个问号"？")。 生成形状**记录集**有两个级别，在其中父占用较高级别，且子占用更低的级别。  
  
 创建子子句**记录集**现在可能嵌套形状的任意数量计算命令，其中的嵌套最深的命令都包含参数化的查询。 生成形状**记录集**具有多个级别，在其中父占用的最高级别、 子占用最下方级别和任意数目的**记录集**s 生成的形状计算命令占用的介入性级别。  
  
 典型用此功能是要调用的聚合函数和 shapeCOMPUTE 分组功能的命令创建中间**记录集**分析有关的信息的子对象**记录集**. 此外，由于这是参数化的形状命令，每次父级的章节列访问时，新的子级**记录集**可能检索。 干预的级别都派生自此子级，因为它们也将重新计算。  
  
## <a name="see-also"></a>请参阅  
 [数据整理示例](../../../ado/guide/data/data-shaping-example.md)
