---
title: ASSL 对象和对象特征 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: be8750b6af60fd1d1bc387d90b9071fc6b282f72
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="assl-objects-and-object-characteristics"></a>ASSL 对象和对象特征
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Analysis Services 脚本语言 (ASSL) 中的对象遵循关于对象组、继承、命名、扩展和处理的特定准则。  
  
## <a name="object-groups"></a>对象组  
 所有[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]对象具有 XML 表示形式。 这些对象分为以下两组：  
  
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
  
-   **CreatedTimestamp**  
  
-   **LastSchemaUpdate**  
  
-   **LastProcessed** （如果适用）  
  
> [!NOTE]  
>  作为主要对象的对象分类将影响 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例处理该对象的方式和以对象定义语言处理该对象的方式。 但是，此分类不保证 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 管理和开发工具允许这些对象的独立创建、修改或删除。  
  
 **次要对象**  
 次要对象只能作为创建、更改或删除父级主要对象操作的组成部分进行创建、修改或删除。 次要对象包括：  
  
-   层次结构和级别  
  
-   属性  
  
-   度量值组  
  
-   挖掘模型列  
  
-   与多维数据集关联的命令  
  
-   Aggregations  
  
## <a name="object-expansion"></a>对象扩展  
 **ObjectExpansion**限制可用于控制度的服务器返回的 ASSL XML 扩展。 此限制具有下表所列的选项。  
  
|枚举值|允许\<Alter >|Description|  
|-----------------------|---------------------------|-----------------|  
|*ReferenceOnly*|否|只返回请求对象以及以递归方式包含的所有主要对象的名称、ID 和时间戳。|  
|*ObjectProperties*|是|展开请求的对象和次要包含对象，但不返回主要包含对象。|  
|*ExpandObject*|否|与相同*ObjectProperties*，但也会返回名称、 ID 以及包含主要对象的时间戳。|  
|*ExpandFull*|是|完全展开请求的对象以及所有以递归方式包含的对象。|  
  
 此 ASSL 参考部分描述*ExpandFull*表示形式。 所有其他**ObjectExpansion**级别均源自此级别。  
  
## <a name="object-processing"></a>对象处理  
 ASSL 包括只读元素或属性 (例如， **LastProcessed**)，它能够读取从[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例，但其将被省略命令脚本提交到的实例时。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 忽略只读元素的已修改值，并且不发出警告或错误。  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 还会忽略不适当或不相关的属性，并且不会引发验证错误。 例如，X 元素只应在 Y 元素有特定值时才存在。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例忽略 X 元素，而不会根据 Y 元素的值验证该元素。  
  
  
