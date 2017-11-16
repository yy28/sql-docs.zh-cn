---
title: "共享数据馈送使用数据馈送的库 (Power Pivot for SharePoint) |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: power-pivot-sharepoint
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data feeds [Analysis Services with SharePoint]
ms.assetid: 4ec98dec-0cd2-4727-bb79-5bf6f8a865d6
caps.latest.revision: 26
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 31457f6abb88dff525bd19609b8dd552adadfeb8
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="share-data-feeds-using-a-data-feed-library-power-pivot-for-sharepoint"></a>使用数据馈送库共享数据馈送 (Power Pivot for SharePoint)
  数据馈送是从以 Atom 线路格式显示数据的服务或应用程序中生成的 XML 数据流。 它越来越多地用于在应用程序之间传输数据以及将数据传输到客户端查看器。 在 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 部署中，数据馈送的作用是使用识别 Atom 的应用程序或服务中的数据填充 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据源。  
  
 如果您已使用识别 Atom 的应用程序组合，则可能始终不需要知道如何生成和使用馈送，因为数据传输是在应用程序之间无缝进行的。 但是，使用自定义解决方案发布 Atom 馈送的组织通常需要一种方法使信息工作者可以获得馈送。 一种方法是创建并共享数据服务文档 (.atomsvc) 文件，此类文件提供到生成馈送的联机源之间的连接。 一个名为数据馈送库的特殊用途库支持在 SharePoint Web 应用程序中创建和共享数据服务文档。  
  
 本主题包含以下各节：  
  
 [先决条件](#prereq)  
  
 [创建数据服务文档](#createdsdoc)  
  
 [保护数据服务文档](#securedsdoc)  
  
 [修改数据服务文档](#modifydsdoc)  
  
 [下一步：使用数据服务文档](#usedsdoc)  
  
> [!NOTE]  
>  虽然数据馈送用于将 Web 数据添加到你在 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 中创建的 [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)]数据源，但可以读取 Atom 馈送的任何客户端应用程序都可以处理数据服务文档。  
  
##  <a name="prereq"></a> 先决条件  
 必须具有将 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 的部署。 通过 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 解决方案包可部署数据馈送支持。  
  
 您必须具有支持数据服务文档内容类型的 SharePoint 库。 建议将默认数据馈送库用于此目的，但您可以手动将内容类型添加到任何库。 有关详细信息，请参阅[创建或自定义数据馈送库 (PowerPivot for SharePoint)](../../analysis-services/power-pivot-sharepoint/create-or-customize-a-data-feed-library-power-pivot-for-sharepoint.md)。  
  
 您必须具有以 Atom 1.0 格式提供 XML 表格数据的数据服务或联机数据源。  
  
 您必须对 SharePoint 站点具有“参与讨论”权限，才能在 SharePoint 库中创建或管理数据服务文档。  
  
##  <a name="createdsdoc"></a> 创建数据服务文档  
 数据服务文档是一个持续的请求，用于根据请求从以馈送格式提供数据的联机数据源或应用程序获得数据流。 当您创建数据服务文档时，应指定一个指针，该指针指向一个或多个以 Atom 联合格式提供 XML 表格数据且 URL 可寻址的数据服务。  
  
 一个文档可以指定多个数据馈送。 如果您要通过单个导入操作从同一服务（或甚至从不同服务）检索一组数据负载，则这非常有用。  
  
1.  在 SharePoint 站点上，打开数据馈送库或另一个您已添加和配置了数据服务内容类型的文档库。 若要查找以前创建的数据馈送库，请单击“快速启动”中的 **“查看全部”** 。  
  
2.  在页顶部功能区的“文档工具”中，单击 **“文档”**。  
  
3.  单击 **“新建文档”** ，然后选择 **“数据服务文档”**。  
  
4.  在“新建数据服务文档”页中，输入以下信息：  
  
    1.  数据服务文档的名称和说明。 确保提供足够的详细信息，以便用户可以确定是否使用该馈送。  
  
    2.  在“数据馈送”中，输入指向以 Atom 1.0 格式提供数据的数据服务或 Web 应用程序的 URL。  
  
         此 URL 必须解析为以行和列形式返回结构化或半结构化数据的服务。 服务应以匿名方式或通过当前用户的安全凭据返回数据。  
  
         URL 必须解析为支持 Windows 身份验证、基本身份验证或匿名访问的服务。 导入馈送的用户指定要使用的方案。 默认情况下，集成安全性处于选中状态。  
  
         数据馈送 URL 可以包含参数。 不同类型的数据服务技术支持高级 URL 寻址方案，使您可以精确选择要使用的数据。 例如，ADO.NET 数据服务提供用于在基础数据中指定实体、关联和导航路径的 URL 参数。 通过指定一个复杂的 URL 作为数据馈送的源，可以精确指定要使用的数据集。  
  
    3.  对于同一数据馈送，输入随后用于在客户端应用程序中标识该数据集的表名称。 在 [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)]中，您导入的每个数据馈送位于 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据源中其自己的表控件中。 当您设置数据馈送时，必须指定用于接收导入数据的表的名称。  
  
5.  单击“添加其他数据馈送”重复上述步骤，以指定来自相同服务或不同服务的其他馈送。  
  
     每个数据服务文档均作为单个操作进行处理。 将以异步方式生成文档中的所有数据馈送，并在同一个操作中将其返回到客户端应用程序。 因此，只为您要一起使用的数据馈送指定“URL-表”对。  
  
     由于身份验证方案是在数据服务文档级别设置的，因此，每个其他数据馈送都必须源自支持将相同身份验证方案作为第一个馈送的服务或应用程序。 将在运行时以相同方法对相同数据服务文档中的所有馈送进行身份验证。  
  
6.  保存文档。 此数据服务文档作为一个物理文件 (.atomsvc) 存储在为此内容类型配置的内容库中。  
  
 若要使用数据服务文档，可以在 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 中打开 [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] 工作簿，并在“导入数据”向导中选择 **“从数据馈送”** 选项。 当系统提示时，用户将指定数据服务文档的 SharePoint URL 以开始数据导入操作。 有关详细信息，请参阅 [使用数据馈送 (PowerPivot for SharePoint)](../../analysis-services/power-pivot-sharepoint/use-data-feeds-power-pivot-for-sharepoint.md)。  
  
##  <a name="securedsdoc"></a> 保护数据服务文档  
 数据服务文档继承包含它的库的权限。 对项设置的权限将确定用户是否可以打开、修改或删除数据服务文档。  
  
 若要在 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 客户端应用程序中将数据服务文档用作数据馈送进行导入，用户只需对文档具有查看权限。 查看权限足以在导入向导中解析 URL。  
  
 仅在数据馈送导入操作开始时，才检查对于数据服务文档的查看权限。 而并不持续检查对于文档的导入后权限；已添加到 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据源的馈送作为静态数据存在，它们已与提供原始连接信息的数据服务文档断开连接。  
  
 同样，您随后计划的任何数据刷新操作也会排除数据服务文档。 导入时，每个馈送的连接信息将被复制到 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据源以用于刷新。 在这种情况下，执行数据刷新时并不检查对于数据服务文档的权限，因为刷新操作中始终不引用文档本身。  
  
|任务|SharePoint 权限要求|  
|----------|----------------------------------------|  
|将数据馈送导入到已启用 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]的工作簿。|针对库中数据服务文档库的查看权限。|  
|在 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 客户端应用程序中，刷新以前通过馈送检索到的数据。|不适用。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 客户端应用程序使用嵌入的 HTTP 连接信息，直接连接到提供馈送的数据服务和应用程序。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 客户端应用程序不使用数据服务文档。|  
|在 SharePoint 场中，作为计划的任务刷新数据，而无需任何用户输入。|不适用。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务使用嵌入的 HTTP 连接信息，直接连接到提供馈送的数据服务和应用程序。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务不使用数据服务文档。|  
|删除库中的数据服务文档|对于库的“参与讨论”权限。|  
  
##  <a name="modifydsdoc"></a> 修改数据服务文档  
 您可以在数据服务文档中添加、编辑或删除各个“URL-表”项。 在保存所做的更改后，在新的导入操作中选择此服务文档的用户将获取您指定的数据馈送。  
  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿不受您所做更改的影响。 这是因为在初始导入操作中，只读取一次数据服务文档。 在导入过程中，复制服务 URL 和表名称并将其存储在工作簿内部。 然后，这些内部值在后续的刷新操作中用于获取更新后的数据。  
  
 因为 SharePoint 站点上的数据服务文档与包含导入馈送的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿之间不存在永久链接，所以，修改数据服务文档的任何部分都不会影响现有 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿。  
  
> [!IMPORTANT]  
>  尽管只读取一次数据服务文档，但可以定期访问提供实际数据的数据服务以获取更新的馈送。 有关如何刷新数据的详细信息，请参阅 [PowerPivot 数据刷新](../../analysis-services/power-pivot-sharepoint/power-pivot-data-refresh.md)。  
  
##  <a name="usedsdoc"></a> 下一步：使用数据服务文档  
 若要使用你在 SharePoint 库中创建的数据服务文档，可以使用 **数据源中的**[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] “从数据馈送”导入选项。 有关说明，请参阅[使用数据馈送 (PowerPivot for SharePoint)](../../analysis-services/power-pivot-sharepoint/use-data-feeds-power-pivot-for-sharepoint.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Power Pivot 数据馈送](../../analysis-services/power-pivot-sharepoint/power-pivot-data-feeds.md)  
  
  

