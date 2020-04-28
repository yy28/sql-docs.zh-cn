---
title: 编辑类型映射（AccessToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 7f9d9530-6c04-41d9-bbe7-d91820a30066
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 7d41fc2f01e2cfbc2b20c58ea9be640f2afd8ea0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68006580"
---
# <a name="edit-type-mapping-accesstosql"></a>编辑类型映射（AccessToSQL）
利用 "**编辑类型映射**" 对话框，您可以指定如何在源数据库对象和目标数据库对象之间映射类型。  
  
可以在以下几个位置访问此对话框：  
  
-   选择源数据库或数据库对象时，"**类型映射**" 选项卡将显示在 "元数据资源管理器" 右侧。 单击 "**添加**" 以添加新的类型映射，或者单击 "**编辑**" 更改现有的类型映射。  
  
-   在 "**工具**" 菜单上，选择 "**项目设置**" 或 "**默认项目设置**"。 在生成的对话框中，选择 "**类型映射**"。 单击 "**添加**" 以添加新的类型映射，或者单击 "**编辑**" 更改现有的类型映射。  
  
表特定的类型映射会重写数据库和项目类型映射。 数据库特定的映射会替代项目映射。  
  
## <a name="options"></a>选项  
**源类型**  
选择要映射到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型的源数据类型。  
  
如果数据类型的长度可变，以下字段将显示在 "**源类型**" 下：  
  
**From**  
指定此映射的最小长度。 例如，对于**文本**数据类型，可以输入10来指定此映射适用于从**文本（10）** 开始的范围。  
  
**功能**  
指定此映射的最大长度。 例如，对于**文本**数据类型，可以输入20来指定此映射适用于以**文本（20）** 结束的范围。  
  
**目标类型**  
选择源[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型要映射到的数据类型。 当 SSMA 在中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]创建表或存储过程时，源数据类型将更改为此数据类型。  
  
如果数据类型的长度可变，以下字段将显示在 "**目标类型**" 下：  
  
**替换为**  
指定此映射的目标长度。 例如，对于**nvarchar**数据类型，可以输入20来指定应将指定的源数据类型映射到**nvarchar （20）**。  
  
