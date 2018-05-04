---
title: 参数化命令使用干预计算命令 |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], parameterized commands
- parameterized commands [ADO]
- APPEND clause [ADO]
- COMPUTE command [ADO]
ms.assetid: 732f624f-8900-4608-9815-194302d22e8b
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2affa34fd504397b045e100ec8f07232d6dfec7e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="parameterized-commands-with-intervening-compute-commands"></a>与中间的参数化的命令计算命令
典型的参数化的形状追加命令具有创建父级的子句**记录集**使用一个查询命令和创建子级的另一个子句**记录集**使用参数化的查询命令-即包含参数占位符的命令 (一个问号"？")。 调整所生成**记录集**具有两个级别，在其中父占用较高级别，且子占用较低的级别。  
  
 创建子子句**记录集**现在可能任意数目的嵌套形状计算命令，其中的嵌套最深的命令都包含参数化的查询。 调整所生成**记录集**具有多个级别，在其中父占用的最顶部的级别，子占据调换级别和任意数目的**记录集**由生成的 s形状计算命令占用中间层。  
  
 典型使用此功能是调用的聚合函数和分组功能 shapeCOMPUTE 命令创建干扰**记录集**分析信息有关子对象**记录集**. 此外，由于这是参数化的形状命令，每次父级的章节列访问时，新的子级**记录集**可能检索。 因为从子派生中间层，它们还将重新计算。  
  
## <a name="see-also"></a>另请参阅  
 [数据整理示例](../../../ado/guide/data/data-shaping-example.md)
