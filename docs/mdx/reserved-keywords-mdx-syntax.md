---
title: 保留关键字 （MDX 语法） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d88e78e49a52919ff710cd123ab2b25022aa5d1b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68037057"
---
# <a name="reserved-keywords-mdx-syntax"></a>保留关键字（MDX 语法）


  Analysis Services 保留其独占使用的某些关键字。 有关保留关键字的列表，请参阅[MDX 保留字](../mdx/mdx-reserved-words.md)。  
  
 保留关键字遵循下列指导原则：  
  
-   除了 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 定义的位置外，不能在多维表达式 (MDX) 语句中的任何位置包含保留关键字。  
  
-   数据库中任何对象都不能指定与保留关键字相同的名称。 如果存在这样的名称，必须始终使用分隔标识符来引用这个对象。 虽然此方法允许对象名称与保留关键字相同，但应尽量避免使用关键字来命名对象。  
  
-   请使用能避免使用保留关键字的命名约定。 如果对象名称必须与某个保留关键字类似，则可以删除辅音或元音。  
  
## <a name="see-also"></a>请参阅  
 [MDX 语法元素&#40;MDX&#41;](../mdx/mdx-syntax-elements-mdx.md)  
  
  
