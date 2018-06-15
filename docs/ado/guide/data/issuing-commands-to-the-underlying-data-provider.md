---
title: 对基础数据提供程序发出命令 |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- underlying providers [ADO]
- data shaping [ADO], commands
ms.assetid: d6001863-7733-4c32-817f-081e48587fa1
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5a2e18440c651a65da820cf2f2d51b00ae98e92d
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35271946"
---
# <a name="issuing-commands-to-the-underlying-data-provider"></a>对基础数据提供程序发出命令
不会以开头形状任何命令传递到的数据提供程序。 这相当于颁发窗体"SHAPE {提供程序命令}"中的形状命令。 这些命令执行*不*必须生成**记录集**。 例如，"形状 {放表 MyTable} 是一个完全有效形状命令，假定数据提供程序支持 DROP TABLE。  
  
 此功能允许正常的提供程序命令和 shape 命令均使用相同的连接和事务。  
  
## <a name="see-also"></a>请参阅  
 [调整示例数据](../../../ado/guide/data/data-shaping-example.md)   
 [正式形状语法](../../../ado/guide/data/formal-shape-grammar.md)   
 [常用 Shape 命令](../../../ado/guide/data/shape-commands-in-general.md)
