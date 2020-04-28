---
title: 转换设置（MySQLToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f551cf6e-1575-4206-9cca-975b5b43a6b8
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: debdd549dc010f7be6b9d9b37a4caf649d4e106a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68103126"
---
# <a name="conversion-settings-mysqltosql"></a>转换设置 (MySQLToSQL)
**"设置"** 选项卡允许用户设置节点级别设置。 选项卡将在以下元数据库节点上提供：  
  
-   数据库节点  
  
-   函数类别  
  
-   Function 节点  
  
-   表类别  
  
-   表节点  
  
## <a name="specifications"></a>规格  
"**设置**" 选项卡有两个用户设置，即。：  
  
1.  函数转换  
  
2.  表转换  
  
这些设置将基于元数据库节点的类型提供。 例如，函数转换相关设置将在表节点上不可用  
  
> [!NOTE]  
> -   用户所做的更改将作为单独的首选项文件保存在 "项目" 工作区中。  
> -   此文件的扩展名将为**ccprefs**。  
  
1.  **函数转换设置：**  
  
    1.  此选项卡包含 **"强制函数转换"** 选项。 选项可以具有以下四个值之一：  
  
        -   根据项目设置进行转换 [继承]  
  
        -   始终转换为函数  
  
        -   始终转换为过程  
  
        -   根据项目设置进行转换  
  
    2.  根据设置，函数将转换为函数或存储过程。  
  
    3.  单击 "**应用**" 按钮后，用户所做的设置将保存在级联首选项文件中。  
  
2.  **表转换设置：**  
  
    1.  此选项卡包含 **"取消 ROWID 辅助列生成"** 选项。 选项可以具有以下四个值之一：  
  
        -   根据项目设置进行转换 [继承]  
  
        -   是  
  
        -   否  
  
        -   根据项目设置进行转换  
  
    2.  如果**是 "Yes"**，则此设置禁止在目标表上创建 ROWID 辅助列。  
  
    3.  单击 "**应用**" 按钮后，用户所做的设置将保存在级联首选项文件中。  
  
## <a name="see-also"></a>另请参阅  
[项目设置（转换）（MySQL 到 SQL）](https://msdn.microsoft.com/7ad5fe44-6445-4ba8-a457-5af792631f11)  
  
