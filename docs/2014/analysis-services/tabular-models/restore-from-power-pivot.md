---
title: 从 PowerPivot 还原 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql11.asvs.ssmsimbi.RestoreFromPP.f1
ms.assetid: 232ac8ed-77fe-47d8-acd3-59bc2fdfdf48
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f90ea08269e79e57c623af41fc2f0fbc09e2fb42
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66066639"
---
# <a name="restore-from-powerpivot"></a>从 PowerPivot 还原
  您可以使用 SQL Server Management Studio 中的“从 PowerPivot 还原”功能针对 Analysis Services 实例（在表格模式下运行）创建新的表格模型数据库，或从 PowerPivot 工作簿 (.xlsx) 还原到现有数据库。  
  
> [!NOTE]  
>  SQL Server Data Tools 中的“从 PowerPivot 导入”项目模板提供了类似功能。 有关详细信息，请参阅[从 PowerPivot 导入&#40;SSAS 表格&#41;](import-from-power-pivot-ssas-tabular.md)。  
  
 使用“从 PowerPivot 还原”时，请注意下列问题：  
  
-   为了使用“从 PowerPivot 还原”，您必须以该 Analysis Services 实例上的服务器管理员角色的成员身份登录。  
  
-   该 Analysis Services 实例服务帐户必须对您要还原的工作簿文件具有读取权限。  
  
-   默认情况下，当您从 PowerPivot 还原数据库时，表格模型数据库的“数据源模拟信息”属性设置为“默认”，这会指定 Analysis Services 实例服务帐户。 建议在“数据库属性”中将模拟凭据更改为 Windows 用户帐户。 有关详细信息，请参阅[模拟（SSAS 表格）](impersonation-ssas-tabular.md)。  
  
-   PowerPivot 数据模型中的数据将复制到该 Analysis Services 实例上的现有或新的表格模型数据库中。 如果您的 PowerPivot 工作簿包含链接表，则将以不带数据源的表形式来重新创建表，该表与使用“粘贴到新表中”创建的表类似。  
  
### <a name="to-restore-from-powerpivot"></a>从 PowerPivot 还原  
  
1.  在 SSMS 中，你想要还原到的 Active Directory 实例中右键单击**数据库**，然后单击**从 PowerPivot 还原**。  
  
2.  在**从 PowerPivot 还原**对话框中**还原源**，在**备份文件**，单击**浏览**，然后选择.abf 或.xslx若要从还原的文件。  
  
3.  在 **“还原目标”** 中的“ **还原数据库”** 中，键入新数据库或现有数据库的名称。 如果不指定名称，则使用工作簿的名称。  
  
4.  在 **“存储位置”** 中，单击 **“浏览”** ，然后选择数据库的存储位置。  
  
5.  在 **“选项”** 中，选中 **“包括安全信息”** 。 在从 PowerPivot 工作簿还原时，此设置不适用。  
  
## <a name="see-also"></a>请参阅  
 [表格模型数据库（SSAS 表格）](tabular-model-databases-ssas-tabular.md)   
 [从 PowerPivot 导入&#40;SSAS 表格&#41;](import-from-power-pivot-ssas-tabular.md)  
  
  
