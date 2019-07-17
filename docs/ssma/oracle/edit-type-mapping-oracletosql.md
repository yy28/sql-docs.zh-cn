---
title: 编辑类型映射 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 7078b4ed-c779-4bf3-8db8-f9dcb3edd50f
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: b3857d2acda8f5c8b16f416987651db2b6b991b7
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264232"
---
# <a name="edit-type-mapping-oracletosql"></a>编辑类型映射 (OracleToSQL)
**编辑类型映射**对话框可以指定类型的源和目标数据库对象之间的映射方式。  
  
您可以访问此对话框在多个位置：  
  
-   选择源数据库或数据库对象时**类型映射**选项卡上显示的元数据资源管理器的右侧。 单击**外**以添加新的类型映射，或单击**编辑**若要更改现有的类型映射。  
  
-   上**工具**菜单中，选择**项目设置**或**默认项目设置**。 在随后出现的对话框中，选择**类型映射**。 单击**外**以添加新的类型映射，或单击**编辑**若要更改现有的类型映射。  
  
特定于表的类型映射重写数据库和项目类型映射。 特定于数据库的映射覆盖项目映射。  
  
## <a name="options"></a>选项  
**源类型**  
选择源数据类型将映射到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型。  
  
如果数据类型的可变长度，以下字段将显示下**源类型**:  
  
**From**  
指定此映射的最小长度。 例如，对于**nchar**数据类型，可以输入 10，以指定的开始处的范围为此映射**nchar(10)** 。  
  
**To**  
指定此映射的最大长度。 例如，对于**nchar**数据类型，可以输入 20 来指定此映射的结束时间范围**nchar(20)** 。  
  
**目标类型**  
选择[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]源数据类型映射到的数据类型。 SSMA 时创建的表或存储的过程中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，源数据类型将更改为此数据类型。  
  
如果数据类型的可变长度，以下字段将显示下**目标类型**:  
  
**Replace with**  
指定此映射的目标长度。 例如，对于**nvarchar**数据类型，可以输入 20 来指定应将指定的源数据类型映射到**nvarchar(20)** 。  
  
