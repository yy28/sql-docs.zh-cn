---
title: 算术表达式 (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- expressions [XQuery], arithmetic
- arithmetic expressions
ms.assetid: 90d675bf-56da-459a-9771-8cd13920a9fc
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 372ed2a1eb3ecba8f84125ae0231d2110e3966dc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63047581"
---
# <a name="arithmetic-expressions-xquery"></a>算术表达式 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  支持的所有算术运算符，除**idiv**。 以下示例将说明算术运算符的基本用法：  
  
```  
DECLARE @x xml  
SET @x=''  
SELECT @x.query('2 div 2')  
SELECT @x.query('2 * 2')  
```  
  
 因为**idiv**是不受支持，一种解决方案是使用**xs:integer()** 构造函数：  
  
```  
DECLARE @x xml  
SET @x=''  
-- Following will not work  
-- SELECT @x.query('2 idiv 2')  
-- Workaround   
SELECT @x.query('xs:integer(2 div 3)')  
```  
  
 从算术运算符得到的类型基于输入值的类型。 如果操作数为不同类型，则将在需要时根据类型层次结构将一个或两个操作数转换为常用基元基类型。 有关类型层次结构的信息，请参阅[XQuery 中的类型转换规则](../xquery/type-casting-rules-in-xquery.md)。  
  
 如果两个操作为不同的数字基类型，则将产生数字类型升级。 例如，添加**xs: decimal**到**xs: double**会首先将十进制值更改为双精度值。 然后，将执行导致双精度值的添加操作。  
  
 非类型化原子值都转换到另一个操作数的数字基类型，或**xs: double**如果其他操作数也为非类型化。  
  
## <a name="implementation-limitations"></a>实现限制  
 限制如下：  
  
-   算术运算符的参数必须为数值类型或**untypedAtomic**。  
  
-   上的操作**xs: integer**值会导致类型的值**xs: decimal**而不是**xs: integer**。  
  
  
