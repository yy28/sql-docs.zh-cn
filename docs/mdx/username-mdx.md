---
title: UserName (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f1ebb5dc504b799575b2ccf9e47368e4e6511dac
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68097275"
---
# <a name="username-mdx"></a>UserName (MDX)


  返回当前连接的域名和用户名。  
  
## <a name="syntax"></a>语法  
  
```  
  
UserName [ ( ) ]  
```  
  
## <a name="remarks"></a>备注  
 返回值为以下格式的字符串：  
  
 *domain-name\user-name*  
  
## <a name="example"></a>示例  
 下例将返回正在执行查询的用户的用户名。  
  
```  
WITH MEMBER Measures.x AS UserName  
SELECT Measures.x ON COLUMNS  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
