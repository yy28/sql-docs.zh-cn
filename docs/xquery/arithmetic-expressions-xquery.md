---
title: 算术表达式（XQuery） |Microsoft Docs
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
ms.openlocfilehash: ccbeda01726a3473f8e955676c3ebd62a93fd630
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "67985734"
---
# <a name="arithmetic-expressions-xquery"></a>算术表达式 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  除**idiv**外，还支持所有算术运算符。 以下示例将说明算术运算符的基本用法：  
  
```  
DECLARE @x xml  
SET @x=''  
SELECT @x.query('2 div 2')  
SELECT @x.query('2 * 2')  
```  
  
 由于不支持**idiv** ，因此，解决方案是使用**xs： integer （）** 构造函数：  
  
```  
DECLARE @x xml  
SET @x=''  
-- Following will not work  
-- SELECT @x.query('2 idiv 2')  
-- Workaround   
SELECT @x.query('xs:integer(2 div 3)')  
```  
  
 从算术运算符得到的类型基于输入值的类型。 如果操作数为不同类型，则将在需要时根据类型层次结构将一个或两个操作数转换为常用基元基类型。 有关类型层次结构的信息，请参阅[XQuery 中的类型转换规则](../xquery/type-casting-rules-in-xquery.md)。  
  
 如果两个操作为不同的数字基类型，则将产生数字类型升级。 例如，将**xs： decimal**添加到**xs： double**将首先将十进制值更改为双精度值。 然后，将执行导致双精度值的添加操作。  
  
 将非类型化原子值强制转换为另一个操作数的数值基类型，如果另一个操作数也是非类型化的，则为**xs： double** 。  
  
## <a name="implementation-limitations"></a>实现限制  
 限制如下：  
  
-   算术运算符的参数必须是数值类型或**untypedAtomic**。  
  
-   对**xs： integer**值的运算导致类型为**xs： decimal**而不是**xs： integer**类型的值。  
  
  
