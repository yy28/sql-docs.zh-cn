---
title: 规划地图报表（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: dc0c27a4-7e31-4a15-a0bc-3a02479d5b02
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: fd3b765bff38ea006a1dd1a60fe861373715ee80
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37309417"
---
# <a name="plan-a-map-report-report-builder-and-ssrs"></a>规划地图报表（报表生成器和 SSRS）
  好的报表提供的信息可指导您采取措施或让您洞察实际情况。 若要展示分析数据，如某一地理背景下的总销售额或人口统计，您可以将地图添加到报表。 一个地图可以包含多个图层，每个图层都显示由特定类型的空间数据定义的地图元素：代表地点的点、代表路线的线条以及代表区域的多边形。 您可以将分析数据与每个图层上的地图元素相关联。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="MapPurpose"></a> 指定地图的作用  
 良好的报表设计可以提供相关的信息以帮助用户采取措施来解决问题。 若要创建有用的、易于理解的地图显示，请确定您希望地图帮助您回答的问题。 例如，在某个地图上，您可以实现以下数据类型的可视化，以确定市场商机：  
  
-   每个商店的相关销售额。  
  
-   根据相对于商店位置的客户位置，按客户人口统计学分类的销售额。  
  
-   按销售区域划分的比较销售额或其他财务数据。  
  
-   多个商店不同折扣策略的比较销售额。  
  
 在确定地图显示的作用之后，必须分析您需要的数据。 分析数据来自报表数据集。 位置数据来自您必须指定的空间数据源。  
  
 
  
##  <a name="Data"></a> 指定空间数据和分析数据  
 您必须指定您需要哪些空间数据和分析数据。  
  
 分析数据可来自报表数据集，来自与地图库中的地图一起包括的示例数据，或者来自与 ESRI 形状文件中的空间数据一起包括的分析数据。  
  
 空间数据采用三种形式：点、线条和多边形。  
  
-   **点：** 点指定位置，例如，市县或商店、饭馆或会议中心的地址。 对于您要在地图上显示的每个位置，您必须提供该位置的空间数据。 在向地图添加点之后，您可以在点位置显示标记，并改变标记类型、大小和颜色。  
  
-   **线条：** 线条指定路径或路线，例如，交货路线或飞行路径。 在向地图添加线条之后，可以改变线条颜色和线条宽度。  
  
-   **多边形：** 多边形指定区域，例如，地区、领土、国家/地区、省/自治区/直辖市、省、县、市或城市涵盖的地区、邮政编码、电话交换机或人口普查地区。 在向地图添加多边形后，除显示轮廓之外，还可以在多边形区域的中心点显示一个标记。  
  
 在确定需要的空间数据之后，您必须为此数据找到源。  
  
### <a name="find-a-source-for-spatial-data"></a>查找空间数据的源  
 若要找到要在地图中使用的空间数据，可以使用以下源：  
  
-   ESRI 形状文件，包括您可以在 Internet 上搜索的、向公众提供的形状文件。  
  
-   来自 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 空间数据源的空间数据。  
  
-   地图库中报表内的地图。  
  
-   提供空间数据作为 ESRI 形状文件的第三方站点或[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]空间数据。  
  
-   Bing 地图图块，为地图视图提供背景。 若要在地图中显示图块，必须将报表服务器配置为支持 Bing 地图 Web 服务。  
  
 有关详细信息，请参阅 [地图向导和地图层向导（报表生成器和 SSRS）](map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md)中的“在何处可以获取 ESRI 形状文件？”。  
  
 空间数据可能具有政治敏感性，并且可能具有版权。 请检查空间数据源的使用条款和隐私声明，以了解如何在报表中使用空间数据。  
  
 在找到所需的数据后，可以将数据嵌入到报表定义中，或者在处理报表时自动检索此数据。 有关详细信息，请参阅本主题后面的 [在报表定义大小与报表处理时间之间达到平衡](#Embedding) 。  
  
### <a name="determine-the-spatial-data-and-the-spatial-data-match-fields"></a>确定空间数据和空间数据匹配字段  
 若要在地图上显示分析数据并改变大小、颜色或标记类型，必须指定使空间数据与分析数据相关的字段。  
  
 空间数据必须包含以下字段：  
  
-   **Spatial data.** 一个空间数据字段，它具有一系列坐标来定义每个点、线条或多边形。  
  
-   **匹配字段。** 一个或多个唯一标识每个空间数据字段的字段。 例如，对于表示商店位置的点，可以使用商店的名称。 如果商店名称在空间数据中不唯一，则可以包含市县的名称以及商店名称。  
  
 匹配字段用于使空间数据与分析数据相关。  
  
### <a name="determine-the-analytical-data-and-the-analytical-data-match-fields"></a>确定分析数据和分析数据匹配字段  
 在确定空间数据之后，必须确定分析数据。 分析数据可以来自以下源：  
  
-   现有报表数据集。 可以将字段指定为简单字段表达式，例如 [Sales] 或 =Fields!Sales.Value。  
  
-   由空间数据源提供的数据字段。 将字段指定为关键字，它们以 # 开头且后跟来自空间数据源的字段名称。  
  
 然后，必须确定匹配字段的名称：  
  
-   匹配字段。 与空间数据匹配字段指定相同信息的一个或多个字段，用于在空间数据与分析数据之间建立关系。 匹配字段应匹配数据类型以及格式。  
  
 当您已确定空间数据源、空间数据、分析数据源、分析数据和匹配字段时，您就已准备就绪，可以确定要向报表添加哪种类型的地图。  
  

  
##  <a name="MapType"></a> 选择地图类型  
 当您运行“地图”向导时，可以向报表添加地图并添加第一个地图层。 通过向导，可以向报表添加以下地图类型之一：  
  
-   基本图，显示位置而没有关联的分析数据。  
  
-   对于每个地图元素具有一个关联的分析值的地图，例如，每个商店位置的总销售额。  
  
-   对于一个地图元素具有多个关联的分析值的地图，例如，每个商店位置的客户数和总销售额。  
  
 下表对各地图类型进行了说明。 所有地图类型都允许您选择一个控制调色板、边框样式和字体的主题以及显示标签。  
  
|向导图标|层样式|层类型|说明和选项|  
|-----------------|-----------------|----------------|-----------------------------|  
|![rs_MapType_Polygon_Basic](../media/rs-maptype-polygon-basic.gif "rs_MapType_Polygon_Basic")|基本图|Polygon|只显示区域的地图，例如，销售区域。<br /><br /> 选项：通过调色板改变颜色或使用一种颜色。 调色板是一组预定义的颜色。 当分配完调色板中的所有颜色后，将分配颜色的阴影。|  
|![rs_MapType_Polygon_ColorAnalytical](../media/rs-maptype-polygon-coloranalytical.gif "rs_MapType_Polygon_ColorAnalytical")|颜色分析图|Polygon|一个按变化的颜色显示分析数据的地图，例如，按区域列出的销售数据。|  
|![rs_MapType_Polygon_Bubble](../media/rs-maptype-polygon-bubble.gif "rs_MapType_Polygon_Bubble")|气泡图|多边形|一个在各区域中心以不同气泡大小显示分析数据的地图，例如，按区域列出的销售数据。<br /><br /> 选项：根据第二个分析字段改变区域颜色以及指定颜色规则。|  
|![rs_MapType_Line_Basic](../media/rs-maptype-line-basic.gif "rs_MapType_Line_Basic")|基本线条图|行|只显示线条的地图，例如，交货路线。<br /><br /> 选项：通过调色板改变颜色或使用一种颜色。|  
|![rs_MapType_Line_Analytical](../media/rs-maptype-line-analytical.gif "rs_MapType_Line_Analytical")|分析线条图|行|线条颜色和宽度发生变化的地图，例如，交货的包装数和按路线的实时度量。<br /><br /> 选项：通过一个分析字段改变线条宽度，通过第二个分析字段改变线条颜色，以及指定颜色规则。|  
|![rs_MapType_Marker_Basic](../media/rs-maptype-marker-basic.gif "rs_MapType_Marker_Basic")|基本标记地图|点|在每个位置显示一个标记的地图，例如，市县。<br /><br /> 选项：通过调色板改变颜色或使用一种颜色，以及更改标记样式。|  
|![rs_MapType_Marker_Bubble](../media/rs-maptype-marker-bubble.gif "rs_MapType_Marker_Bubble")|气泡标记地图|点|对每个位置显示一个气泡且气泡大小按一个分析数据字段变化的地图，例如，按市县列出的销售数据。<br /><br /> 选项：根据第二个分析字段改变气泡颜色以及指定颜色规则。|  
|![rs_MapType_Marker_Analytical](../media/rs-maptype-marker-analytical.gif "rs_MapType_Marker_Analytical")|分析标记地图|点|在每个位置显示一个标记且标记颜色、大小和类型随分析数据发生变化的地图，例如，最畅销的产品、利润范围和折扣策略。<br /><br /> 选项：通过一个分析字段改变标记类型，通过第二个分析字段改变标记大小，通过第三个分析字段改变标记颜色，以及指定颜色规则。|  
  
 在使用“地图”向导添加地图之后，您可以使用“层”向导创建其他层或更改用于层的选项。 有关向导的详细信息，请参阅[地图向导和地图层向导（报表生成器和 SSRS）](map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md)。  
  
 可以单独为每个层自定义显示或数据选项。 有关运行向导后自定义地图的详细信息，请参阅[自定义地图或地图层的数据和显示（报表生成器和 SSRS）](customize-the-data-and-display-of-a-map-or-map-layer-report-builder-and-ssrs.md)。  
  
 
  
##  <a name="Legend"></a> 规划图例  
 为了帮助用户解释地图，可以添加多个地图图例、一个色阶和一个距离刻度。 当您设计地图时，请规划要在何处显示图例。 可以指定有关每个图例的以下信息：  
  
-   **图例位置。** 例如，图例可以显示在视区内部或外部，并相对于视区显示在 12 个分离的位置。  
  
-   **图例样式**。 例如，可以指定字形、边框样式、分隔线和填充属性。  
  
-   **图例标题。** 例如，您可以指定标题文本，并独立控制是否为图例显示标题以及是否显示色阶。  
  
-   **地图图例布局。** 例如，地图图例可以显示为高表或宽表。  
  
 在报表处理过程中，将根据您为每个层设置的规则选项，自动创建图例的内容。  
  
 默认情况下，所有层都在第一个地图图例中显示规则的结果。 您可以创建多个图例，然后对于每个规则，指定使用哪个图例来显示结果。  
  
 有关详细信息，请参阅[按规则和分析数据更改多边形、线条和点的显示方式（报表生成器和 SSRS）](vary-polygon-line-and-point-display-by-rules-and-analytical-data.md)和[更改地图图例、色阶和关联的规则（报表生成器和 SSRS）](change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs.md)。  
  

  
##  <a name="Embedding"></a> 在报表定义大小与报表处理时间之间达到平衡  
 针对地图的良好报表设计要求您在控制报表性能和报表定义大小的选项之间达到平衡。 基于空间数据或 Bing 地图图块的地图元素可以是静态的且可嵌入到报表定义中；它们也可以是动态的，而在每次处理报表时创建。 必须在静态或动态地图数据之间进行折衷，并找出适合您所在环境的平衡点。 在制定这一决策时，请考虑以下信息：  
  
-   嵌入的地图元素可能显著增加报表定义的大小，但会减少在报表中查看地图所需的时间。 报表服务器可能具有大小限制，您需要注意这一点。  
  
-   报表定义为可以处理的空间数据点数指定限制；同时指定一个单独的值，该值指定可以在报表定义中包含的地图元素的数量。  
  
-   动态地图元素减少报表定义大小，但会增加处理和呈现地图所需的时间。  
  
-   如果空间数据源位于您的计算机上，则地图元素始终嵌入到报表定义中。 这包括来自已在本地安装的地图库或 ESRI 形状文件的空间数据。  
  
 若要使用动态空间数据，空间数据源必须位于报表服务器上。 当在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中设计报表时，可以将空间数据源添加到项目，并将其以及报表定义一起发布到报表服务器。 如果您使用报表生成器来设计报表，必须首先将空间数据上载到报表服务器，然后在向导或层属性中，为该地图层指定此空间数据源。  
  

  
## <a name="see-also"></a>请参阅  
 [自定义地图或地图层的数据和显示（报表生成器和 SSRS）](customize-the-data-and-display-of-a-map-or-map-layer-report-builder-and-ssrs.md)   
 [教程：地图报表（报表生成器）](../tutorial-map-report-report-builder.md)   
 [地图（报表生成器和 SSRS）](maps-report-builder-and-ssrs.md)   
 [报表故障排除： 地图报表&#40;报表生成器和 SSRS&#41;](troubleshoot-reports-map-reports-report-builder-and-ssrs.md)  
  
  
