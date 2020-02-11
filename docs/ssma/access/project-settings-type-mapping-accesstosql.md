---
title: 项目设置（类型映射）（AccessToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access data types
- data types, default mappings
- default data type mappings
- Project Settings dialog box, Type Mapping
- SQL Server data types
- Type Mapping settings
ms.assetid: b87b9683-abed-4677-8c50-18bdba704655
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 01154cf477435e9dc5335606d0c11a05aecc492b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68066661"
---
# <a name="project-settings-type-mapping-accesstosql"></a>项目设置（类型映射）（AccessToSQL）
"类型映射项目设置" 允许您为 SSMA 项目设置默认的类型映射。 还可以为单个数据库对象指定类型映射。 有关详细信息，请参阅[映射源和目标数据类型](mapping-source-and-target-data-types-accesstosql.md)。  
  
"**项目设置**" 和 "**默认项目设置**" 对话框中提供了类型映射：  
  
-   使用 "**项目设置**" 对话框可以设置当前项目的配置选项。 若要访问类型映射设置，请在 "**工具**" 菜单上选择 "**项目设置**"，然后单击左窗格中的 "**类型映射**"。  
  
-   使用 "**默认项目设置**" 对话框可以为所有项目设置配置选项。 若要访问类型映射设置，请在 "**工具**" 菜单上，选择 "**默认项目设置**"，从 "**迁移目标版本**" 下拉框中选择需要查看其设置的 "迁移项目类型"，然后单击左窗格中的 "**类型映射**"。  
  
## <a name="options"></a>选项  
**源类型**  
要映射的 Access 数据类型。  
  
**目标类型**  
指定访问[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型的目标或 SQL Azure 数据类型。  
  
下表显示源和目标数据类型之间的默认映射。  
  
|Access 数据类型|SQL Server 数据类型|  
|--------------------|------------------------|  
|**binary [\*.。\*]**|**varbinary [\*]**|  
|**变量**|**bit**|  
|**位**|**tinyint**|  
|**货币**|**money**|  
|**date**|**datetime**|  
|**Decimal**|**float**|  
|**double**|**float**|  
|**guid**|**uniqueidentifier**|  
|**整数**|**smallint**|  
|**漫长**|**int**|  
|**longbinary**|**varbinary(max)**|  
|**"**|**nvarchar(max)**|  
|**备注**-Access 97|**varchar(max)**|  
|**单个**|**实际上**|  
|**文本 [\*.。\*]**|**nvarchar [\*]**|  
|**文本 [\*.。] \*** -用于访问97|**varchar [\*]**|  
  
**添加**  
单击此可将数据类型添加到 "映射" 列表中。  
  
**编辑**  
单击此项可在 "映射" 列表中编辑数据类型。  
  
**删除**  
单击此选项可从 "映射" 列表中删除所选的数据类型映射。  
  
**重置为默认值**  
单击此设置可将所有数据类型映射重置为 SSMA 默认值。  
  
## <a name="see-also"></a>另请参阅  
[映射源和目标数据类型](mapping-source-and-target-data-types-accesstosql.md)  
[用户界面参考（访问）](https://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
