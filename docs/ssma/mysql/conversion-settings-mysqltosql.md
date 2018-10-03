---
title: 转换设置 (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f551cf6e-1575-4206-9cca-975b5b43a6b8
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: a311b35597b3c474c2128e73b148ab882f19f42c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47732315"
---
# <a name="conversion-settings-mysqltosql"></a>转换设置 (MySQLToSQL)
**设置**选项卡允许用户设置节点级别设置。 选项卡将出现在以下元数据库节点：  
  
-   数据库节点  
  
-   函数类别  
  
-   函数节点  
  
-   表类别  
  
-   表节点  
  
## <a name="specifications"></a>规范：  
**设置**选项卡有两个用户设置，报道。:  
  
1.  从函数转换  
  
2.  表转换  
  
这些设置将提供基于元数据库节点的类型。 例如，函数转换相关的设置将不可用在表节点  
  
> [!NOTE]  
> -   用户所做的更改将保存在项目工作区中，作为单独的首选项文件。  
> -   将此文件的扩展名**ccprefs**。  
  
1.  **函数转换设置：**  
  
    1.  此选项卡包含**强制函数转换**选项。 该选项可以具有以下四个值之一：  
  
        -   根据项目设置 [继承] 转换  
  
        -   始终将转换为一个函数  
  
        -   始终将转换为一个过程  
  
        -   根据项目设置将转换  
  
    2.  根据设置，该函数将转换到一个函数或存储过程。  
  
    3.  在单击的级联首选项文件中保存用户所做的设置**应用**按钮。  
  
2.  **表转换设置：**  
  
    1.  此选项卡包含**禁止显示 ROWID 辅助列生成**选项。 该选项可以具有以下四个值之一：  
  
        -   根据项目设置 [继承] 转换  
  
        -   用户帐户控制  
  
        -   否  
  
        -   根据项目设置将转换  
  
    2.  如果**是**，此设置禁止 ROWID 辅助列创建对目标表的创建。  
  
    3.  由用户所做的设置保存在级联首选项文件，方法是单击**应用**按钮。  
  
## <a name="see-also"></a>请参阅  
[项目设置 （转换） （mysql 迁移到 SQL）](http://msdn.microsoft.com/en-us/7ad5fe44-6445-4ba8-a457-5af792631f11)  
  
