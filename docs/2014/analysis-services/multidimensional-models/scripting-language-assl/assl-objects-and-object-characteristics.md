---
title: ASSL 对象和对象特征 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- reference exceptions [Analysis Services Scripting Language]
- ASSL, objects
- inheritance [Analysis Services Scripting Language]
- localized names [Analysis Services Scripting Language]
- objects [Analysis Services Scripting Language]
- names [Analysis Services Scripting Language]
- Analysis Services Scripting Language, objects
- expansion [Analysis Services Scripting Language]
ms.assetid: 6e5c28b5-c0bc-4ccd-82e5-e174bbb71386
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: aee5e7b94aaaca2b35e34f8c4d49c2834189f114
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62736611"
---
# <a name="assl-objects-and-object-characteristics"></a>ASSL 对象和对象特征
  Analysis Services 脚本语言 (ASSL) 中的对象遵循关于对象组、继承、命名、扩展和处理的特定准则。  
  
## <a name="object-groups"></a>对象组  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]所有[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]对象均具有 XML 表示形式。 这些对象分为以下两组：  
  
 **主要对象**  
 可以单独创建、更改和删除主要对象。 主要对象包括：  
  
-   服务器  
  
-   数据库  
  
-   维度  
  
-   多维数据集  
  
-   度量值组  
  
-   分区  
  
-   透视  
  
-   挖掘模型  
  
-   角色  
  
-   与服务器或数据库关联的命令  
  
-   数据源  
  
 主要对象具有以下可跟踪其历史记录和状态的属性。  
  
-   `CreatedTimestamp`  
  
-   `LastSchemaUpdate`  
  
-   `LastProcessed`（视具体情况而定）  
  
> [!NOTE]  
>  作为主要对象的对象分类将影响 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例处理该对象的方式和以对象定义语言处理该对象的方式。 但是，此分类不保证 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 管理和开发工具允许这些对象的独立创建、修改或删除。  
  
 **次要对象**  
 次要对象只能作为创建、更改或删除父级主要对象操作的组成部分进行创建、修改或删除。 次要对象包括：  
  
-   层次结构和级别  
  
-   特性  
  
-   度量值组  
  
-   挖掘模型列  
  
-   与多维数据集关联的命令  
  
-   Aggregations  
  
## <a name="object-expansion"></a>对象扩展  
 `ObjectExpansion` 限制可用于控制服务器返回的 ASSL XML 扩展的程度。 此限制具有下表所列的选项。  
  
|枚举值|允许\<Alter>|说明|  
|-----------------------|---------------------------|-----------------|  
|*ReferenceOnly*|否|只返回请求对象以及以递归方式包含的所有主要对象的名称、ID 和时间戳。|  
|*ObjectProperties*|是|展开请求的对象和次要包含对象，但不返回主要包含对象。|  
|*ExpandObject*|否|与*ObjectProperties*相同，但还返回包含的主要对象的名称、ID 和时间戳。|  
|*Updateoptions.expandfull*|是|完全展开请求的对象以及所有以递归方式包含的对象。|  
  
 此 ASSL 参考部分介绍了*updateoptions.expandfull*的表示形式。 所有其他 `ObjectExpansion` 级别都派生自此级别。  
  
## <a name="object-processing"></a>对象处理  
 ASSL 包含只读元素或属性（例如 `LastProcessed`），这些元素或属性可从 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例读取，但在向该实例提交命令脚本时将被忽略。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 忽略只读元素的已修改值，并且不发出警告或错误。  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 还会忽略不适当或不相关的属性，并且不会引发验证错误。 例如，X 元素只应在 Y 元素有特定值时才存在。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例忽略 X 元素，而不会根据 Y 元素的值验证该元素。  
  
  
