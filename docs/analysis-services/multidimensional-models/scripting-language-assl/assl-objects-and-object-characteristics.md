---
title: ASSL 对象和对象特征 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 55150d0835fc0a9e3324acfb8007a1d22e9b55d8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208499"
---
# <a name="assl-objects-and-object-characteristics"></a>ASSL 对象和对象特征
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Analysis Services 脚本语言 (ASSL) 中的对象遵循关于对象组、继承、命名、扩展和处理的特定准则。  
  
## <a name="object-groups"></a>对象组  
 所有[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]对象都有 XML 表示形式。 这些对象分为以下两组：  
  
 **主要对象**  
 可以单独创建、更改和删除主要对象。 主要对象包括：  
  
-   服务器  
  
-   数据库  
  
-   维度  
  
-   多维数据集  
  
-   度量值组  
  
-   “度量值组”  
  
-   透视  
  
-   挖掘模型  
  
-   角色  
  
-   与服务器或数据库关联的命令  
  
-   数据源  
  
 主要对象具有以下可跟踪其历史记录和状态的属性。  
  
-   **CreatedTimestamp**  
  
-   **LastSchemaUpdate**  
  
-   **LastProcessed** （如果适用）  
  
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
 **ObjectExpansion**限制可用于控制服务器返回的 ASSL XML 扩展的程度。 此限制具有下表所列的选项。  
  
|枚举值|允许\<更改 >|描述|  
|-----------------------|---------------------------|-----------------|  
|*ReferenceOnly*|否|只返回请求对象以及以递归方式包含的所有主要对象的名称、ID 和时间戳。|  
|*ObjectProperties*|是|展开请求的对象和次要包含对象，但不返回主要包含对象。|  
|*ExpandObject*|否|与相同*ObjectProperties*，但也会返回名称、 ID 和所包含主要对象的时间戳。|  
|*ExpandFull*|是|完全展开请求的对象以及所有以递归方式包含的对象。|  
  
 本 ASSL 参考部分介绍*ExpandFull*表示形式。 所有其他**ObjectExpansion**级别派生自此级别。  
  
## <a name="object-processing"></a>对象处理  
 ASSL 包含只读元素或属性 (例如， **LastProcessed**)，可以从读取[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例，但命令脚本提交到的实例时将被忽略。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 忽略只读元素的已修改值，并且不发出警告或错误。  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 还会忽略不适当或不相关的属性，并且不会引发验证错误。 例如，X 元素只应在 Y 元素有特定值时才存在。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例忽略 X 元素，而不会根据 Y 元素的值验证该元素。  
  
  
