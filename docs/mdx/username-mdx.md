---
title: "用户名 (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- UserName
dev_langs:
- kbMDX
helpviewer_keywords:
- UserName function
ms.assetid: ecae549b-5c5e-4483-84e6-b713cd297d7e
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e9d9dbf069eab4da9c06e1a387baba47a90c24c5
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="username-mdx"></a>UserName (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回当前连接的域名和用户名。  
  
## <a name="syntax"></a>語法  
  
```  
  
UserName [ ( ) ]  
```  
  
## <a name="remarks"></a>注释  
 返回值为以下格式的字符串：  
  
 *域名 \ 用户名*  
  
## <a name="example"></a>示例  
 下例将返回正在执行查询的用户的用户名。  
  
```  
WITH MEMBER Measures.x AS UserName  
SELECT Measures.x ON COLUMNS  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

