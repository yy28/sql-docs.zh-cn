---
description: 向基础数据提供程序发出命令
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 6d9000fdf63a908257c9dbdfa29dc7b57dbb7ecf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453229"
---
# <a name="issuing-commands-to-the-underlying-data-provider"></a>向基础数据提供程序发出命令
不以 SHAPE 开头的任何命令都将传递给数据访问接口。 这等效于使用 "SHAPE {provider command}" 形式发出形状命令。 这些命令 *无* 需生成 **记录集**。 例如，如果数据访问接口支持 DROP TABLE，则 "SHAPE {DROP TABLE MyTable} 是一个完全有效的形状" 命令。  
  
 此功能允许普通提供程序命令和形状命令共享相同的连接和事务。  
  
## <a name="see-also"></a>另请参阅  
 [数据定形示例](../../../ado/guide/data/data-shaping-example.md)   
 [正式形状语法](../../../ado/guide/data/formal-shape-grammar.md)   
 [常用 Shape 命令](../../../ado/guide/data/shape-commands-in-general.md)
