---
title: "项目设置 （类型映射） (AccessToSQL) |Microsoft 文档"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Access data types
- data types, default mappings
- default data type mappings
- Project Settings dialog box, Type Mapping
- SQL Server data types
- Type Mapping settings
ms.assetid: b87b9683-abed-4677-8c50-18bdba704655
caps.latest.revision: 16
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: f1fbca03968ed7257cd7b65a42a6fff5180dbedc
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="project-settings-type-mapping-accesstosql"></a>项目设置 （类型映射） (AccessToSQL)
类型映射的项目设置，可以设置 SSMA 项目的默认类型映射。 你还可以指定单个数据库对象的类型映射。 有关详细信息，请参阅[映射源和目标数据类型](http://msdn.microsoft.com/en-us/b362a075-16e7-423f-b63f-e1e9f02844a9)。  
  
类型映射可用于**项目设置**和**默认项目设置**对话框：  
  
-   使用**项目设置**对话框可设置为当前项目的配置选项。 若要访问的类型映射设置，在**工具**菜单上，选择**项目设置**，然后单击**类型映射**的左窗格中。  
  
-   使用**默认项目设置**对话框中设置的所有项目的配置选项。 若要访问的类型映射设置，在**工具**菜单上，选择**默认项目设置**，选择为其设置所需查看 / 更改，不再是迁移项目类型**迁移目标版本**下拉列表中，然后单击**类型映射**的左窗格中。  
  
## <a name="options"></a>选项  
**源类型**  
要映射的访问的数据类型。  
  
**目标类型**  
目标[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或指定的访问的数据类型的 SQL Azure 数据类型。  
  
下表显示源和目标数据类型之间的默认映射。  
  
|访问数据类型|SQL Server 数据类型|  
|--------------------|------------------------|  
|**二进制 [\*...\*]**|**varbinary [\*]**|  
|**boolean**|**bit**|  
|**字节**|**tinyint**|  
|**货币**|**money**|  
|**date**|**datetime**|  
|**decimal**|**float**|  
|**double**|**float**|  
|**guid**|**uniqueidentifier**|  
|**integer**|**int**|  
|**长**|**int**|  
|**长二进制**|**varbinary(max)**|  
|**备注**|**nvarchar(max)**|  
|**备注**-对于 Access 97|**varchar(max)**|  
|**单个**|**real**|  
|**text[\*..\*]**|**nvarchar [\*]**|  
|**text[\*..\*]** -对于 Access 97|**varchar [\*]**|  
  
**“添加”**  
单击此项可将数据类型添加到映射列表。  
  
**编辑**  
单击此项可编辑的映射列表中的数据类型。  
  
**删除**  
单击以从映射列表中删除所选的数据类型映射。  
  
**重置为默认值**  
单击以将所有数据类型映射重都置为 SSMA 默认值。  
  
## <a name="see-also"></a>另请参阅  
[映射源和目标数据类型](http://msdn.microsoft.com/en-us/b362a075-16e7-423f-b63f-e1e9f02844a9)  
[用户界面 Reference(Access)](http://msdn.microsoft.com/en-us/af24c303-4a41-449b-9c86-d6558a97e839)  
  

