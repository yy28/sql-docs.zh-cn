---
title: 向基础数据提供程序发出命令 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- underlying providers [ADO]
- data shaping [ADO], commands
ms.assetid: d6001863-7733-4c32-817f-081e48587fa1
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 231d9ced5bf370b8ee7c507e930e6961cfbed5a8
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700576"
---
# <a name="issuing-commands-to-the-underlying-data-provider"></a>向基础数据提供程序发出命令
不会开始形状与任何命令传递到的数据提供程序。 这相当于发出窗体"形状 {提供程序命令}"中的形状命令。 这些命令执行*不*需要生成**记录集**。 例如，"形状 {下拉表 MyTable} 是一个完全有效形状命令，假定数据提供程序支持删除表。  
  
 此功能允许正常的提供程序命令和 shape 命令共享相同的连接和事务。  
  
## <a name="see-also"></a>请参阅  
 [数据整理示例](../../../ado/guide/data/data-shaping-example.md)   
 [正式 Shape 语法](../../../ado/guide/data/formal-shape-grammar.md)   
 [常用 Shape 命令](../../../ado/guide/data/shape-commands-in-general.md)
