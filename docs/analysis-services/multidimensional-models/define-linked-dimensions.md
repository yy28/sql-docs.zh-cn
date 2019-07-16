---
title: 定义链接的维度 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8441f37d902c823e9d8dce27a96b2d78f3f38b26
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "68209016"
---
# <a name="define-linked-dimensions"></a>定义链接维度
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  链接维度基于在具有相同版本和兼容性级别的另一个 Analysis Services 数据库中创建和存储的维度。 通过使用链接维度，您可以创建、存储以及维护某个数据库上的维度，同时可让多个数据库的用户使用该维度。 对于用户，链接维度在外观上就像其他任意维度一样。  
  
 链接文档是只读的。 如果您想要修改维度或创建新关系，则必须更改源维度，然后删除后再重新创建链接的维度及其关系。 不能刷新某一链接的维度以便从源项目中提取更改。  
  
 所有相关的度量值组和维度必须都来自相同的源数据库。 不能在本地度量值组和您添加到多维数据集的链接文档之间创建新关系。 将链接维度和度量值组添加到当前多维数据集后，必须在其源数据库中维护它们之间的关系。  
  
> [!NOTE]  
>  因为刷新功能不可用，所以，大多数 Analysis Services 开发人员都是复制维度，而不是链接它们。 可以跨同一个解决方案中的多个项目复制维度。 有关详细信息，请参阅 [在 SSAS 中刷新链接的维度](http://sqlblog.com/blogs/marco_russo/archive/2006/09/12/refresh-of-a-linked-dimension-in-ssas.aspx)。  
  
## <a name="prerequisites"></a>先决条件  
 提供维度的源数据库和使用维度的当前数据库必须处于相同的版本和兼容级别。 有关详细信息，请参阅 [多维数据库的兼容级别 (Analysis Services)](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)。  
  
 源数据库必须已部署并且处于联机状态。 发布或恢复链接对象的服务器必须配置为允许该操作（见下文）。  
  
 您想要使用的维度本身不能是链接维度。  
  
## <a name="configure-server-to-allow-linked-objects"></a>配置服务器以便允许链接对象  
  
1.  在 SQL Server Management Studio 中，连接到 Analysis Services 服务器。 在对象资源管理器中，右键单击服务器名称，然后选择“方面”  。  
  
2.  将 **LinkedObjectsLinksFromOtherInstancesEnabled** 设置为 **True** ，以便允许服务器对驻留在运行于其他实例上的数据库中的链接对象发出请求。  
  
3.  将 **LinkedObjectsLinksToOtherInstances** 设置为 **True** ，以便允许服务器请求链接到正在其他实例上运行的数据库的数据。  
  
## <a name="create-a-linked-dimension-in-sql-server-data-tools"></a>在 SQL Server Data Tools 中创建链接维度  
  
1.  启动向导。 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中，右键单击 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库或项目中的“维度”  文件夹，然后单击“新建链接维度”  。  
  
2.  连接到提供维度的 Analysis Services 数据库。 在链接对象向导的 **“选择数据源”** 页中，选择 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据源或创建一个新数据源。  
  
3.  在向导的 **“选择对象”** 页中，选择指向远程数据库链接中的维度。  
  
4.  在 **“完成向导”** 页中，可以预览链接对象。 如果链接的维度与已经存在的维度同名，则将在该名称后追加一个序号（从“1”开始，“1”表示第一个重复名称）。 完成向导后，该维度将添加到 **“维度”** 文件夹中。  
  
##  <a name="bkmk_CreateNew"></a> 创建与 Analysis Services 数据库的新数据源连接  
 使用“新建数据源”向导以便添加到与提供维度的 Analysis Services 数据库有关的项目连接信息。 您可以通过在“链接对象”向导的“选择数据源”页中单击 **“新建数据源”** ，启用该向导。  
  
1.  在“数据源”向导中的“选择如何定义连接”页上，单击 **“新建”** 。  
  
2.  在连接管理器中，确保提供程序设置为“本机 OLE DB\Microsoft OLE DB Provider for Analysis Services 11.0”  。  
  
3.  输入服务器的名称（将 servername\\instancename 用于已命名实例   ），或键入 **localhost** 以便连接到在同一台计算机上正在运行的 Analysis Services 服务器。  
  
4.  使用 Windows 身份验证进行连接。  
  
5.  在 **“初始目录”** 中，单击向下箭头以选择此服务器上的数据库。  
  
6.  在“数据源向导”中，单击 **“下一步”** 以继续。  
  
7.  在“模拟信息”页中，单击 **“使用服务帐户”** 。 单击 **“下一步”** ，然后完成向导。 将在“链接对象”向导中选择您刚定义的连接。  
  
## <a name="next-steps"></a>后续步骤  
 您不能更改链接维度的结构，因此无法使用维度设计器的 **“维度结构”** 选项卡来进行查看。 处理链接维度后，可以使用 **“浏览器”** 选项卡进行查看。还可以更改维度的名称，并为该名称创建一个转换。  
  
## <a name="see-also"></a>请参阅  
 [多维数据库的兼容级别 (Analysis Services)](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)   
 [链接度量值组](../../analysis-services/multidimensional-models/linked-measure-groups.md)   
 [维度关系](../../analysis-services/multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)  
  
  
