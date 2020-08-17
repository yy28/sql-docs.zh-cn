---
description: Instr (MDX)
title: Instr (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 877fc4658081108e810e404dfc8d4a368c6964ba
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387353"
---
# <a name="instr-mdx"></a>Instr (MDX)


  返回一个字符串在另一字符串中第一次出现的位置。  
  
## <a name="syntax"></a>语法  
  
```  
InStr([start, ]searched_string, search_string[, compare])  
```  
  
## <a name="arguments"></a>参数  
 *start*  
 （可选）设置每个搜索的起始位置的一个数值表达式。 如果省略此值，则搜索将会在第一个字符位置开始。 如果 start 为 null，则函数返回值未定义。  
  
 *searched_string*  
 要搜索的字符串表达式。  
  
 *search_string*  
 要对其进行搜索的字符串表达式。  
  
 *比较*  
 （可选）一个整数值。 始终忽略此参数。 定义它是为了与其他语言中的其他 **Instr** 函数兼容。  
  
## <a name="return-value"></a>返回值  
 以*string1*开头位置为*string2*的整数值。  
  
 此外， **InStr** 函数返回下表中列出的值，具体取决于条件：  
  
|条件|返回值|  
|---------------|------------------|  
|String1 为零长度|零 (0)|  
|String1 为 Null|undefined|  
|String2 为零长度|start|  
|String2 为 Null|undefined|  
|找不到 String2|零 (0)|  
|start 大于 Len(String2)|零 (0)|  
  
## <a name="remarks"></a>备注  
  
> [!WARNING]  
>  **Instr** 始终执行不区分大小写的比较。  
  
## <a name="example"></a>示例  
 下面的示例演示如何使用 **Instr** 函数并显示不同的结果方案。  
  
```  
with   
    member [Date].[Date].[Results] as "Results"  
    member measures.[lowercase found in lowercase string] as InStr( "abcdefghijklmnñopqrstuvwxyz", "o")  
    member measures.[uppercase found in lowercase string] as InStr( "abcdefghijklmnñopqrstuvwxyz", "O")  
    member measures.[searched string is empty]            as InStr( "", "o")  
    member measures.[searched string is null]             as iif(IsError(InStr( null, "o")), "Is Error", iif(IsNull(InStr( null, "o")), "Is Null","Is undefined"))  
    member measures.[search string is empty]              as InStr( "abcdefghijklmnñopqrstuvwxyz", "")  
    member measures.[search string is empty start 10]     as InStr(10, "abcdefghijklmnñopqrstuvwxyz", "")  
    member measures.[search string is null]               as iif(IsError(InStr( null, "o")), "Is Error", iif(IsNull(InStr( null, "o")), "Is Null","Is undefined"))  
    member measures.[found from start 10]                 as InStr( 10, "abcdefghijklmnñopqrstuvwxyz", "o")  
    member measures.[NOT found from start 17]             as InStr( 17, "abcdefghijklmnñopqrstuvwxyz", "o")  
    member measures.[NULL start]                          as iif(IsError(InStr( null, "abcdefghijklmnñopqrstuvwxyz", "o")), "Is Error", iif(IsNull(InStr( null, "abcdefghijklmnñopqrstuvwxyz", "o")), "Is Null","Is undefined"))  
    member measures.[start greater than searched length]  as InStr( 170, "abcdefghijklmnñopqrstuvwxyz", "o")  
  
select  [Results] on columns,  
       { measures.[lowercase found in lowercase string]  
       , measures.[uppercase found in lowercase string]  
       , measures.[searched string is empty]  
       , measures.[searched string is null]  
       , measures.[search string is empty]  
       , measures.[search string is empty start 10]  
       , measures.[search string is null]  
       , measures.[found from start 10]  
       , measures.[NOT found from start 17]  
       , measures.[NULL start]   
       , measures.[start greater than searched length]  
       } on rows  
  
from [Adventure Works]  
```  
  
 下表显示了获得的结果。  
  
|度量值中的字段|结果|  
|-|-|  
|lowercase found in lowercase string|16|  
|uppercase found in lowercase string|16|  
|searched string is empty|0|  
|searched string is null|未定义|  
|search string is empty|1|  
|search string is empty start 10|10|  
|search string is null|未定义|  
|found from start 10|16|  
|NOT found from start 17|0|  
|NULL start|未定义|  
|start greater than searched length|0|  
  
  
