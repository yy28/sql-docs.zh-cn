---
title: 编辑类型映射 (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f93c4b7d-74fc-4856-bf42-035289918e83
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 47e1321802b237f02a63535572b1850dbb4c74f6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63299263"
---
# <a name="edit-type-mapping-db2tosql"></a>编辑类型映射 (DB2ToSQL)
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
指定此映射的最小长度。 例如，对于**nchar**数据类型，可以输入 10，以指定的开始处的范围为此映射**nchar(10)**。  
  
**若要**  
指定此映射的最大长度。 例如，对于**nchar**数据类型，可以输入 20 来指定此映射的结束时间范围**nchar(20)**。  
  
**目标类型**  
选择[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]源数据类型映射到的数据类型。 SSMA 时创建的表或存储的过程中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，源数据类型将更改为此数据类型。  
  
如果数据类型的可变长度，以下字段将显示下**目标类型**:  
  
**Replace with**  
指定此映射的目标长度。 例如，对于**nvarchar**数据类型，可以输入 20 来指定应将指定的源数据类型映射到**nvarchar(20)**。  
  
