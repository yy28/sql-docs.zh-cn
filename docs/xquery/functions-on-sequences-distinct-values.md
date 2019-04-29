---
title: 非重复值函数 (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- distinct-values function
- fn:distinct-values function
ms.assetid: f4c2bb53-2bec-4f1a-9c00-cf997fb7ae5b
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 48b338416b7bd464a69c424354f4029c719fef33
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62939090"
---
# <a name="functions-on-sequences---distinct-values"></a>基于序列的函数 - distinct-values
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  删除重复的值从指定的序列 *$arg*。 如果 *$arg*是一个空序列，该函数将返回空序列。  
  
## <a name="syntax"></a>语法  
  
```  
  
fn:distinct-values($arg as xdt:anyAtomicType*) as xdt:anyAtomicType*  
```  
  
## <a name="arguments"></a>参数  
 *$arg*  
 原子值序列。  
  
## <a name="remarks"></a>备注  
 所有类型的原子化值传递给**distinct-values （)** 必须是同一基类型的子类型。 接受的基类型是支持的类型**eq**操作。 这些类型包括三种内置数值基类型、日期/时间基类型、xs:string、xs:boolean 和 xdt:untypedAtomic。 类型 xdt:untypedAtomic 的值转换为 xs:string。 如果这些类型混合在一起，或者传递了其他类型的其他值，则会引发静态错误。  
  
 结果**distinct-values （)** 接收带有原始基数的传入的类型，例如 untypedatomic xs: string 的基类型。 如果输入在静态上为空，则暗示为空，并且会引发静态错误。  
  
 类型 xs:string 的值与 XQuery 默认 Unicode 码位排序规则进行比较。  
  
## <a name="examples"></a>示例  
 本主题提供了一些针对 XML 实例存储在各种中的 XQuery 示例**xml**类型列中的 AdventureWorks 数据库。  
  
### <a name="a-using-the-distinct-values-function-to-remove-duplicate-values-from-the-sequence"></a>A. 使用 distinct-values() 函数从序列中删除重复的值  
 在此示例中，包含电话号码的 XML 实例分配给**xml**类型的变量。 针对此变量使用指定的 XQuery **distinct-values （)** 函数编译不包含重复项的电话号码的列表。  
  
```  
declare @x xml  
set @x = '<PhoneNumbers>  
 <Number>111-111-1111</Number>  
 <Number>111-111-1111</Number>  
 <Number>222-222-2222</Number>  
</PhoneNumbers>'  
-- 1st select  
select @x.query('  
  distinct-values( data(/PhoneNumbers/Number) )  
') as result  
```  
  
 下面是结果：  
  
```  
111-111-1111 222-222-2222    
```  
  
 在以下查询中，一系列数字 （1，1，2） 传递给**distinct-values （)** 函数。 然后函数将删除序列中重复的数字并返回剩下的两个数字。  
  
```  
declare @x xml  
set @x = ''  
select @x.query('  
  distinct-values((1, 1, 2))  
') as result  
```  
  
 该查询将返回 1 2。  
  
### <a name="implementation-limitations"></a>实现限制  
 限制如下：  
  
-   **Distinct-values （)** 函数将整数值映射到 xs: decimal。  
  
-   **Distinct-values （)** 函数仅支持以前提及的类型，不支持基类型的混合。  
  
-   **Distinct-values （)** 不支持对 xs: duration 值的函数。  
  
-   不支持提供排序规则的语法选项。  
  
## <a name="see-also"></a>请参阅  
 [针对 xml 数据类型的 XQuery 函数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
