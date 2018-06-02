---
title: 保留关键字 （MDX 语法） |Microsoft 文档
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b82117f17ecc1d7b98648a6641dc697b2fd40b9c
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2018
ms.locfileid: "34582259"
---
# <a name="reserved-keywords-mdx-syntax"></a>保留关键字（MDX 语法）
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 保留供其独占使用某些关键字。 有关保留关键字的列表，请参阅[MDX 保留字](../mdx/mdx-reserved-words.md)。  
  
 保留关键字遵循下列指导原则：  
  
-   除了 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 定义的位置外，不能在多维表达式 (MDX) 语句中的任何位置包含保留关键字。  
  
-   数据库中任何对象都不能指定与保留关键字相同的名称。 如果存在这样的名称，必须始终使用分隔标识符来引用这个对象。 虽然此方法允许对象名称与保留关键字相同，但应尽量避免使用关键字来命名对象。  
  
-   请使用能避免使用保留关键字的命名约定。 如果对象名称必须与某个保留关键字类似，则可以删除辅音或元音。  
  
## <a name="see-also"></a>请参阅  
 [MDX 语法元素&#40;MDX&#41;](../mdx/mdx-syntax-elements-mdx.md)  
  
  
