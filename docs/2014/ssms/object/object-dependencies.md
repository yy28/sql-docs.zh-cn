---
title: 对象依赖关系 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.swb.common.objectdependencies.f1
ms.assetid: c63d1160-3f3d-45df-99be-6fe081125fb5
author: stevestein
ms.author: sstein
ms.openlocfilehash: 02fadc1b87393e02d1ff27f9596d6d7677e23cb3
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85058621"
---
# <a name="object-dependencies"></a>对象依赖关系
  一些数据库对象与其他数据库对象存在依赖关系。 例如，视图和存储过程依赖于包含视图或过程返回的数据的表是否存在。 当前对象的“对象依赖关系（‘常规’页）”  列出了该对象正常运行所需的数据库对象和依赖于所选对象的对象。 在其定义中引用了另一个对象并且该定义存储在系统目录中的对象称为“引用实体”  。 被另一对象引用的对象称为“被引用实体”  。  
  
 当前对象的“对象依赖关系（‘高级’页）”  列出了依赖于该对象的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库对象和 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 对象。 这些对象可存储于不同的服务器上。  
  
 使用此对话框可在更改或删除所选对象之前了解其依赖关系。  
  
## <a name="ui-element-list"></a>UI 元素列表  
 **依赖对象**  _\<selected object>_  
 单击此按钮将列出依赖于所选对象的对象，以及依赖关系跟踪所涉及的对象。  
  
 **对象** _\<selected object>_**取决于**      
 单击此按钮将列出所选对象所依赖的并且依赖关系跟踪涉及的对象。  
  
 **依赖项**  
 如果单击了“依赖  **的对象”** _\<selected object>_ ，则选择此选项将显示依赖于所选对象的对象的层次结构视图。 如果单击了“ **依赖的对象”** _\<selected object>_  ，则选择此选项将显示所选对象所依赖的对象的层次结构视图。  
  
 **名称**  
 显示上面“依赖关系”  树视图中所选对象的名称。  
  
 类型   
 显示上面“依赖关系”  树视图中所选对象的类型。  
  
 **上次同步时间**  
 > [!NOTE]  
>  仅在“高级”  页上提供此选项。  
  
 指定上次更新依赖关系信息的时间和日期。  
  
 **依赖关系类型**  
 > [!NOTE]  
>  仅在“常规”  页上提供此选项。  
  
 显示两个对象之间的依赖关系的类型。 可以是以下值之一：  
  
-   架构绑定依赖关系  
  
     是两个对象之间的一种关系，只要引用对象存在，这种关系就可防止删除或修改被引用的对象。 当通过使用 WITH SCHEMABINDING 子句创建视图或用户定义的函数时，或者当表通过 CHECK 或 DEFAULT 约束或在计算列的定义中引用另一对象时，将创建架构绑定依赖关系。  
  
-   非架构绑定依赖关系  
  
     是两个对象之间的一种关系，这种关系不能防止删除或修改被引用的对象。  
  
-   不可用或未解析的实体  
  
     指示无法确定依赖关系的类型。 只有所选对象位于早于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]实例上时才会出现这种情况。  
  
  
