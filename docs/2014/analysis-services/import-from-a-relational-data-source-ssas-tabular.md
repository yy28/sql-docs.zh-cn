---
title: 从关系数据源 (SSAS 表格) 导入 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 043201cc-fbef-4ed0-bde8-dc5e3a3e8bea
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 44c4f0a5fbdaa64f2145113bf5135dad9acbddbb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48167507"
---
# <a name="import-from-a-relational-data-source-ssas-tabular"></a>从关系数据源导入（SSAS 表格）
  通过使用表导入向导，你可以从各种关系数据库导入数据。 该向导在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]的“模型”菜单中提供  。 若要连接到数据源，必须在计算机上安装适当的访问接口。 有关支持的数据源和提供程序的详细信息，请参阅[支持的数据源（SSAS 表格）](tabular-models/data-sources-supported-ssas-tabular.md)。  
  
 “表导入向导”支持从以下数据源中导入数据：  
  
 **关系数据库**  
  
-   Microsoft SQL Server 数据库  
  
-   Microsoft SQL Azure  
  
-   Microsoft Access 数据库  
  
-   Microsoft SQL Server Parallel Data Warehouse  
  
-   Oracle  
  
-   Teradata  
  
-   Sybase  
  
-   Informix  
  
-   IBM DB2  
  
-   OLE DB/ODBC  
  
 **多维源**  
  
-   Microsoft SQL Server Analysis Services 多维数据集  
  
 “表导入向导”不支持从作为数据源的 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 工作簿导入数据。  
  
### <a name="to-import-data-from-a-database"></a>从数据库导入数据  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，单击 **“模型”** 菜单，然后单击 **“从数据源导入”**。  
  
2.  在 **“连接数据源”** 页中，选择要连接到的数据库的类型，然后单击 **“下一步”**。  
  
3.  执行表导入向导中的步骤。 在后续页上，您可以使用 **“选择表和视图”** 页或在 **“指定 SQL 查询”** 页上创建 SQL 查询来选择特定表和视图或者应用筛选器。  
  
## <a name="see-also"></a>请参阅  
 [导入数据&#40;SSAS 表格&#41;](import-data-ssas-tabular.md)   
 [支持的数据源（SSAS 表格）](tabular-models/data-sources-supported-ssas-tabular.md)  
  
  
