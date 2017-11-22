---
title: "转换设置 (MySQLToSQL) |Microsoft 文档"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: f551cf6e-1575-4206-9cca-975b5b43a6b8
caps.latest.revision: "10"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 29e0343f6f4e254a8171cb1d44084201af34d7d9
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="conversion-settings-mysqltosql"></a>转换设置 (MySQLToSQL)
**设置**选项卡允许用户级别设置节点。 选项卡将出现在以下的元数据库节点：  
  
-   数据库节点  
  
-   函数类别  
  
-   函数节点  
  
-   表类别  
  
-   表节点  
  
## <a name="specifications"></a>规范：  
**设置** 选项卡具有两个用户设置，viz。:  
  
1.  函数转换  
  
2.  表转换  
  
这些设置将提供基于元数据库节点的类型。 例如，函数转换相关的设置将不可用在表节点  
  
> [!NOTE]  
> -   用户所做的更改将保存在项目工作区中，为单独的首选项文件。  
> -   此文件扩展名将为**ccprefs**。  
  
1.  **函数转换设置：**  
  
    1.  此选项卡包含**'强行函数转换'**选项。 该选项可以具有以下四个值之一：  
  
        -   根据项目设置 [继承] 转换  
  
        -   始终将转换为函数  
  
        -   始终将转换为过程  
  
        -   根据项目设置将转换  
  
    2.  根据设置，该函数将转换到一个函数或存储过程。  
  
    3.  用户所做的这些设置保存在单击的级联首选项文件**应用**按钮。  
  
2.  **表转换设置：**  
  
    1.  此选项卡包含**禁止显示 ROWID 辅助列生成**选项。 该选项可以具有以下四个值之一：  
  
        -   根据项目设置 [继承] 转换  
  
        -   是  
  
        -   是  
  
        -   根据项目设置将转换  
  
    2.  如果**是**，此设置禁止创建目标表上创建的 ROWID 辅助列。  
  
    3.  用户所做的设置保存在单击的级联首选项文件**应用**按钮。  
  
## <a name="see-also"></a>另请参阅  
[项目设置 （转换） (MySQL to SQL)](http://msdn.microsoft.com/en-us/7ad5fe44-6445-4ba8-a457-5af792631f11)  
  
