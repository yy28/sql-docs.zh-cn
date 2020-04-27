---
title: 清除 "Analysis Services 缓存 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 6bf66fdd-6a03-4cea-b7e2-eb676ff276ff
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e35ee4b59c77c3d1b47db360d11a9b838106c1b4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66080294"
---
# <a name="clear-the-analysis-services-caches"></a>清除 Analysis Services 缓存
  Analysis Services 通过缓存数据来提高查询性能。 本主题提供关于使用 XMLA ClearCache 命令来清除为响应 MDX 查询而创建的缓存的建议。 根据您使用的表格模型还是多维模型，运行 ClearCache 的影响有所不同。  
  
 **何时清除多维模型的缓存**  
  
 对于多维数据库，在对计算求值时 Analysis Services 会在公式引擎中生成缓存，并在存储引擎中为维度查询和度量值组查询的结果生成缓存。 当公式引擎需要单元坐标或子多维数据集的度量值数据时，就会发生度量值组查询。 当查询非自然层次结构以及应用 autoexists 时，就会发生维度查询。  
  
 在执行性能测试时，建议清除缓存。 通过在运行的各次测试之间清除缓存，您可以确保缓存不会影响用来测量查询设计更改的影响的任何测试结果。  
  
 **何时清除表格模型的缓存**  
  
 表格模型通常存储在内存中，执行查询时会在内存中执行聚合和其他计算。 因此，ClearCache 命令对表格模型影响有限。 对于表格模型，如果对数据运行 MDX 查询，则可以将这些数据添加到 Analysis Services 缓存中。 特别是，MDX 和 autoexists 操作引用的 DAX 度量值可分别将结果缓存在公式缓存和维度缓存中。 但是请注意，非自然层次结构和度量值组查询不在存储引擎中缓存结果。 此外，必须认识到 DAX 查询不在公式和存储引擎中缓存结果。 如果将缓存引申为是 MDX 查询的结果，对表格模型运行 ClearCache 将使系统中的所有缓存数据失效。  
  
 运行 ClearCache 也将清除 xVelocity 内存中分析引擎 (VertiPaq) 中的内存中缓存。 xVelocity 引擎保持着较小的一组缓存结果。 运行 ClearCache 将使 xVelocity 引擎中的这些缓存失效。  
  
 最后，运行 ClearCache 还将删除为 `DirectQuery` 模式重新配置表格模型时残留在内存中的数据。 这在模型包含需要严格控制的敏感数据时尤为重要。 在这种情况下，运行 ClearCache 是一项预防措施，可确保敏感数据不会存放在不当位置。 如果正在使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 部署模型并更改查询模式，则必须手动清除缓存。 相反，若使用 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 对模型和分区指定 `DirectQuery`，则可以在将模型切换为使用该查询模式时自动清除缓存。  
  
 与清除性能测试期间的多维模型缓存的建议相比，清除表格模型缓存并没有更多的建议。 如果并未管理包含敏感数据的表格模型的部署，则不需要执行特定的管理任务来调用清除缓存操作。  
  
## <a name="clear-the-cache-for-analysis-services-models"></a>清除 Analysis Services 模型的缓存  
 若要清除缓存，请使用 XMLA 和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 您可以在数据库、多维数据集、维度/表或度量值组级别清除缓存。 以下用于在数据库级别清除缓存的步骤同时适用于多维模型和表格模型。  
  
> [!NOTE]  
>  严格的性能测试可能要求更全面的方法来清除缓存。 有关如何刷新 Analysis Services 和文件系统缓存的说明，请参阅 [SQL Server 2008 R2 Analysis Services 操作指南](https://go.microsoft.com/fwlink/?linkID=https://go.microsoft.com/fwlink/?LinkID=225539)中关于清除缓存的一节。  
  
 对于多维和表格模型，清除某些缓存可以遵循一个两步过程，首先是在执行 ClearCache 时使缓存失效，然后在收到下一个查询时清空该缓存。 只有在真正清空缓存后，才会明显减少内存占用。  
  
 清除缓存要求您向 XMLA 查询中的 `ClearCache` 语句提供对象标识符。 本主题中的第一步解释如何获取对象标识符。  
  
#### <a name="step-1-get-the-object-identifier"></a>第 1 步：获取对象标识符  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，右键单击某个对象，选择“属性”，然后复制“属性”窗格中 ID 属性的值********。 这种方法适用于数据库、多维数据集、维度或表。  
  
2.  若要获取度量值组 ID，请右键单击该度量值组并选择“编写度量值组脚本为”****。 选择 **“创建”** 或 **“更改”**，并将查询发送到一个窗口。 度量值组的 ID 将在对象定义中可见。 复制对象定义的 ID。  
  
#### <a name="step-2-run-the-query"></a>第 2 步：运行查询  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，右键单击某个数据库，指向“新建查询”，然后选择 XMLA********。  
  
2.  将以下代码示例复制到 XMLA 查询窗口中。 将 `DatabaseID` 更改为当前连接的数据库的 ID。  
  
    ```  
    <ClearCache xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
      <Object>  
        <DatabaseID> Adventure Works DW Multidimensional</DatabaseID>  
      </Object>  
    </ClearCache>  
  
    ```  
  
     或者，您可以指定子对象（如度量值组）的路径，以便仅清除该对象的缓存。  
  
    ```  
    <ClearCache xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
      <Object>  
        <DatabaseID>Adventure Works DW Multidimensional</DatabaseID>  
            <CubeID>Adventure Works</CubeID>  
            <MeasureGroupID>Fact Currency Rate</MeasureGroupID>  
      </Object>  
    </ClearCache>  
    ```  
  
3.  按 F5 执行该查询。 您应看到以下结果：  
  
    ```  
    <return xmlns="urn:schemas-microsoft-com:xml-analysis">  
      <root xmlns="urn:schemas-microsoft-com:xml-analysis:empty" />  
    </return>  
    ```  
  
## <a name="see-also"></a>另请参阅  
 [在 Analysis Services 中编写管理任务脚本](../script-administrative-tasks-in-analysis-services.md)   
 [监视 Analysis Services 实例](monitor-an-analysis-services-instance.md)  
  
  
