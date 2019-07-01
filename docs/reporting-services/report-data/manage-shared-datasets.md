---
title: 管理共享数据集 | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: 2cbb1fa3-959e-4df6-9887-ebc93cc1b686
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 332103dd9f100a2477b9ae7392bd6d24088261f6
ms.sourcegitcommit: 1bbbbb8686745a520543ac26c4d4f6abe1b167ea
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2019
ms.locfileid: "67220589"
---
# <a name="manage-shared-datasets"></a>管理共享数据集
  在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中，共享数据集从连接到外部数据源的共享数据源中检索数据。 共享数据集提供可共享查询的方法，以便为多个报表提供一组一致的数据。 数据集查询可以包括数据集参数。 您可以配置共享数据集，以便在首次使用时或通过指定计划为特定的参数组合缓存查询结果。 您可以将共享数据集缓存与报表缓存和报表数据馈送结合使用，以便管理对数据源的访问。  
  
 共享数据集仅使用共享数据源，而不使用嵌入数据源。 共享数据集可以基于支持的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 数据扩展插件的任何数据源或基于报表模型。  
  
## <a name="creating-and-using-shared-datasets"></a>创建和使用共享数据集  
 若要创建共享数据集，必须使用创建共享数据集定义文件 (.rsd) 的应用程序。 可以使用以下应用程序之一来创建共享数据集：  
  
-   报表生成器   使用共享数据集设计模式并将共享数据集保存到某一报表服务器或 SharePoint 站点。  
  
-   报表设计器在[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]/ Visual Studio 解决方案资源管理器中的数据集文件夹中创建共享数据集。 若要发布某一共享数据集，请将其部署到报表服务器或 SharePoint 站点。  
  
-   上传共享数据集定义 (.rsd) 文件   你可以将某一文件上传到报表服务器或 SharePoint 站点。 在 SharePoint 站点上。 在缓存共享数据集或者在报表中使用共享数据集之前，不根据架构对上载的文件进行验证。  
  
 共享数据集定义包括查询、包括默认值在内的数据集参数、是否区分大小写之类的数据选项以及数据集筛选器。 只要在报表中包括共享数据集，就使用在定义中设置的值。  
  
 若要在报表中使用某一共享数据集，请打开报表生成器之类的应用程序，浏览到报表服务器或 SharePoint 站点，然后选择该共享数据集。 这会将共享数据集的一个实例添加到报表。 在报表中，不能查看或更改该共享数据集的查询或共享数据源。 您可以指定应用于报表中该实例的一组附加的数据集属性值。 例如，您可以添加筛选器或更改是否区分大小写之类的数据选项。 有关详细信息，请参阅 [报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)。  
  
## <a name="managing-shared-datasets"></a>管理共享数据集  
 若要管理已发布共享数据集的属性，可以使用本机模式报表服务器的 Web 门户，也可以使用 SharePoint 站点上的应用程序页（如果是在 SharePoint 集成模式下部署报表服务器的话）。 您可以对共享数据集执行的任务取决于您的角色分配以及网站级别和项级别权限，包括针对文件夹的权限（如果权限继承有效）。 针对共享数据集的项级别安全性与针对报表的项级别安全性遵循相同的模型。 有关详细信息，请参阅 [保护共享数据集项](../../reporting-services/security/secure-shared-dataset-items.md)。  
  
 您可以独立于使用共享数据集或者它所依赖的共享数据源的报表来管理共享数据集项属性，包括要使用的共享数据源。 若要更改查询或作为共享数据集定义一部分的其他数据集属性，您必须编辑该定义。  
  
### <a name="manage-shared-dataset-item-properties"></a>管理共享数据集项属性  
 下表列出了可为共享数据集项更改的项属性。  
  
|||  
|-|-|  
|编辑名称|更改共享数据集的名称。 来自依赖项的所有引用将继续有效。|  
|编辑说明|更改共享数据集的说明。|  
|编辑查询执行超时值|以秒为单位设置查询执行超时值。 零 (0) 秒表示没有超时。确定数据集查询超时之前等待的秒数。若要指定无超时值，则使用 0。 有关详细信息，请参阅[为报表和共享数据集处理设置超时值 (SSRS)](../../reporting-services/report-server/setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md)。|  
|查看依赖项|查看使用此共享数据集的项：已发布的报表部件、共享数据源和报表。|  
  
 下面的其他共享数据集属性将自动配置：  
  
|属性|描述|  
|--------------|-----------------|  
|HasDataSourceCredentials|相关联的共享数据源是否将凭据保存在报表服务器上。|  
|HasUserProfileDependencies|报表在其查询或筛选表达式中是否具有对“用户”全局集合的引用。|  
  
## <a name="viewing-or-changing-the-shared-dataset-definition"></a>查看或更改共享数据集定义  
 共享数据集属性（包括查询、数据集参数、默认值、数据集筛选器以及诸如排序规则和区分大小写之类的数据选项）保存在共享数据集定义中。 如果您具有足够的权限，则可以查看和更改该定义。  
  
 若要查看或更改共享数据集定义，请在共享数据集设计模式下，在报表生成器之类的应用程序中编辑共享数据集。 在进行更改后，将共享数据集定义保存回服务器或站点。  
  
 在 XML 中查看共享数据集定义的另一种方法是，在 Web 门户中使用 URL 访问语法。 例如，若要查看每个数据集参数的默认值，您可以使用以下 URL 访问命令显示报表服务器上名为 DataSet1 的共享数据集定义：  
  
## <a name="controlling-access-to-the-shared-dataset-definition"></a>控制对共享数据集定义的访问  
 默认情况下，以下任务应用于针对共享数据集的操作。  
  
-   **查看报表** 查看共享数据集项和项属性。  
  
-   **使用报表** 读取共享数据集定义。  
  
-   **管理报表** 创建和删除共享数据集和编辑共享数据集属性。  
  
-   **设置项的安全性** 查看和修改共享数据集的安全设置。  
  
 有关哪些任务和权限可控制对本机模式报表服务器上的数据源属性的访问的详细信息，请参阅 [保护共享数据集项](../../reporting-services/security/secure-shared-dataset-items.md)。  
  
 查看和编辑 SharePoint 库中项属性的权限由站点管理员确定。 有关详细信息，请参阅 [报表服务器项的 SharePoint 站点和列表权限参考](../../reporting-services/security/sharepoint-site-and-list-permission-reference-for-report-server-items.md)。  
  
## <a name="how-to-work-with-shared-dataset-properties-on-a-report-server"></a>如何在报表服务器上使用共享数据集属性  
 您可以使用各种工具来处理共享数据集。 下表汇总了这些方法和工具，并提供指向其他说明的链接。  
  
|任务      |工具      |链接      |  
|----------|----------|----------|  
|添加共享数据集或更改共享数据集定义属性。|在报表生成器中保存。<br /><br /> 在报表设计器中部署。<br /><br /> 上载.rsd 文件中的 web 门户|[报表内嵌数据集和共享数据集（报表生成器和 SSRS）](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)]<br /><br /> [在报表服务器中上传文件或报表](../../reporting-services/reports/upload-a-file-or-report-report-manager.md)<br /><br /> 如果您首先上载一个共享数据集，然后发布该共享数据集所依赖的共享数据源，则必须手动将该共享数据集绑定到该共享数据源。 有关详细信息，请参阅[.../..使用共享数据集-web 门户 /reporting-services/Work](../work-with-shared-datasets-web-portal.md)。|  
|更改共享数据集的项属性。|Web 门户|[使用共享数据集 - Web 门户](../../reporting-services/work-with-shared-datasets-web-portal.md)|  
|为报表中的共享数据集实例指定其他共享数据集属性。|报表生成器/报表设计器|[“数据集属性”对话框 >“查询”（报表生成器）](../../reporting-services/report-data/dataset-properties-dialog-box-query-report-builder.md)|  
|绑定到共享数据集的不同共享数据源。|Web 门户|[配置分页报表的数据源属性 - SSRS](../../reporting-services/report-data/configure-data-source-properties-for-a-report-report-manager.md)|  
|确认数据集参数的默认值。|在报表生成器中打开或使用 URL 访问语法。|例如：<br /><br /> `https://localhost/reportserver/?/Datasets/Dataset1&rs:command=GetShareddatasetDefinition`
|启用缓存|Web 门户|[缓存共享数据集 (SSRS)](../../reporting-services/report-server/cache-shared-datasets-ssrs.md)|  
|创建或编辑缓存刷新计划|Web 门户|[缓存共享数据集](../../reporting-services/report-server/cache-a-shared-dataset.md)|  
|在 SharePoint 集成模式下，同步报表服务器和 SharePoint 站点之间的共享数据集定义|SharePoint 应用程序页|更改共享数据集的项属性<br /><br /> 更改缓存选项<br /><br /> 更改共享数据源|  
  
## <a name="comparing-shared-datasets-with-other-report-server-items"></a>将共享数据集与其他报表服务器项进行比较  
 当您在报表服务器上管理多种类型的项时，理解这些项在哪些方面相似以及它们与其他报表服务器项有什么不同会对您有所帮助。  
  
 共享数据集在以下方面类似于共享数据源和报表：  
  
-   与共享数据源类似，可以独立于使用共享数据集的报表来管理共享数据集。 在报表服务器上管理共享数据集的一部分工作就是能够不必编辑共享数据集定义，便可更改它所依赖的共享数据源。  
  
-   与报表类似，可以缓存共享数据集。 数据源所要求的凭据必须满足缓存限制，并且必须为每个参数指定默认值。 有关详细信息，请参阅 msdn.microsoft.com 上 [缓存共享数据集 (SSRS)](../../reporting-services/report-server/cache-shared-datasets-ssrs.md)。  
  
-   与报表类似，每次进行处理时，都将使用报表服务器上项的当前定义。 如果您对某一共享数据集进行更改，则在处理报表时，使用该共享数据集的每个报表都将使用报表服务器上的当前定义。 如果为共享数据集启用了缓存并且您对共享数据集定义进行更改，则在缓存中的数据到期前，将不使用这些更改。 您可以使用缓存刷新计划来帮助为多个报表提供一致的数据集。  
  
 共享数据集在以下方面有别于已发布的报表部件：  
  
-   与已发布的报表部件不同，当在报表创作客户端中打开报表时，对报表服务器上的共享数据集定义进行更改不会触发更新通知。 在您运行报表时，将使用报表服务器上当前共享数据集定义中的数据。  
  
 共享数据集在以下方面与订阅相似：  
  
-   共享数据集可使用项特定的计划和共享计划进行缓存。  
  
-   在指定参数值时，共享数据集与订阅遵循相同的规则。  
  
## <a name="see-also"></a>另请参阅  
 [报表服务器内容管理（SSRS 本机模式）](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [授予对本机模式报表服务器的权限](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
  
