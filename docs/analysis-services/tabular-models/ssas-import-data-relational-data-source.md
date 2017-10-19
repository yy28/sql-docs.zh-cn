---
title: "从关系数据源 (SSAS 表格) 导入 |Microsoft 文档"
ms.custom: 
ms.date: 10/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 043201cc-fbef-4ed0-bde8-dc5e3a3e8bea
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: d45d72ca09a8abce6d29f018fcbaa8f54415a637
ms.contentlocale: zh-cn
ms.lasthandoff: 10/17/2017

---
# <a name="import-data---relational-data-source"></a>导入数据的关系数据源
  对于 1200 表格模型和较低的兼容性级别，你可以使用导入数据从各种关系数据库表导入向导。 该向导在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]的“模型”菜单中提供  。 若要连接到数据源，必须在计算机上安装适当的访问接口。 有关支持的数据源和提供程序的详细信息，请参阅 [支持的数据源（SSAS 表格）](../../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)。 
 
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
  
 “表导入向导”不支持从作为数据源的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿导入数据。  
  
### <a name="to-import-data-from-a-database"></a>从数据库导入数据  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，单击 **“模型”** 菜单，然后单击 **“从数据源导入”**。  
  
2.  在 **“连接数据源”** 页中，选择要连接到的数据库的类型，然后单击 **“下一步”**。  
  
3.  执行表导入向导中的步骤。 在后续页上，您可以使用 **“选择表和视图”** 页或在 **“指定 SQL 查询”** 页上创建 SQL 查询来选择特定表和视图或者应用筛选器。  
  
## <a name="see-also"></a>另请参阅  
 [导入数据（SSAS 表格）](http://msdn.microsoft.com/library/6617b2a2-9f69-433e-89e0-4c5dc92982cf)   
 [支持的数据源（SSAS 表格）](../../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)  
  
  

