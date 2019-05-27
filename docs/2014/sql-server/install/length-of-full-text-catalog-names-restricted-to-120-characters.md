---
title: 全文本目录名称的长度限制为 120 个字符 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- full-text catalogs names
ms.assetid: 50633373-83f6-4ed9-99b9-71f92479a14f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5cce05426fdff2aacf40612738ad80b07d9ec0e2
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66094054"
---
# <a name="length-of-full-text-catalog-names-restricted-to-120-characters"></a>全文目录名称的长度不能超过 120 个字符
  全文目录名称的最大长度均不能超过 120 个字符，与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以前版本中的 128 个字符限制相比有所减少。  
  
## <a name="description"></a>Description  
 此更改不会影响现有的目录名称，但是如果脚本创建的全文目录的名称长度超过 120 个字符，则会导致错误。 目录名称用于生成与目录对应的逻辑文件名。  
  
## <a name="corrective-action"></a>纠正措施  
 修改所有创建全文目录的脚本，以确保目录名称的长度不超过 120 个字符。  
  
## <a name="see-also"></a>请参阅  
 [使用升级顾问](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
