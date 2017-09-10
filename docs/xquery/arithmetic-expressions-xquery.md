---
title: "算术表达式 (XQuery) |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- expressions [XQuery], arithmetic
- arithmetic expressions
ms.assetid: 90d675bf-56da-459a-9771-8cd13920a9fc
caps.latest.revision: 16
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6ba5c642195f1049f7df59a0fa14ef666eec4bfe
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="arithmetic-expressions-xquery"></a>算术表达式 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  支持所有算术运算符，除**idiv**。 以下示例将说明算术运算符的基本用法：  
  
```  
DECLARE @x xml  
SET @x=''  
SELECT @x.query('2 div 2')  
SELECT @x.query('2 * 2')  
```  
  
 因为**idiv**是不受支持，解决方案是使用**xs:integer()**构造函数：  
  
```  
DECLARE @x xml  
SET @x=''  
-- Following will not work  
-- SELECT @x.query('2 idiv 2')  
-- Workaround   
SELECT @x.query('xs:integer(2 div 3)')  
```  
  
 从算术运算符得到的类型基于输入值的类型。 如果操作数为不同类型，则将在需要时根据类型层次结构将一个或两个操作数转换为常用基元基类型。 有关类型层次结构的信息，请参阅[在 XQuery 中的类型转换规则](../xquery/type-casting-rules-in-xquery.md)。  
  
 如果两个操作为不同的数字基类型，则将产生数字类型升级。 例如，添加**xs: decimal**到**将 xs: double**将首先将十进制值更改为双精度值。 然后，将执行导致双精度值的添加操作。  
  
 非类型化的原子值都转换为另一个操作数的数值基类型，或设置为**将 xs: double**如果另一个操作数还是非类型化。  
  
## <a name="implementation-limitations"></a>实现限制  
 限制如下：  
  
-   对于算术运算符的参数必须是数值类型或**untypedAtomic**。  
  
-   对操作**xs:integer**值导致类型的值**xs: decimal**而不是**xs:integer**。  
  
  
