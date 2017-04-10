---
title: "OData 源 | Microsoft Docs"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.DTS.DESIGNER.ODATASOURCE.F1"
ms.assetid: cc9003c9-638e-432b-867e-e949d50cec90
caps.latest.revision: 14
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 14
---
# OData 源
  在 SSIS 包中使用 OData 源组件可以使用开放数据协议 (OData) 服务中的数据。 该组件支持 OData v3 和 v4 协议。  
  
-   对于 OData V3 协议，该组件支持 ATOM 和 JSON 数据格式。  
  
-   对于 OData V4 协议，该组件支持 JSON 数据格式。  
  
> [!NOTE]  
>  你还可以使用 OData 源读取 SharePoint 列表中的内容。 若要查看 SharePoint 服务器上的所有列表，请使用以下 URL：http://\<server>/_vti_bin/ListData.svc。 有关 SharePoint URL 约定的详细信息，请参阅 [SharePoint Foundation REST 接口](http://msdn.microsoft.com/library/ff521587.aspx)。  OData 源现支持 Microsoft Dynamics AX Online 和 Microsoft Dynamics CRM Online 产品。
  
## <a name="odata-format"></a>OData 格式  
 大多数 OData 服务采用多种格式返回结果。 可以使用 $format 查询选项指定结果集的格式。 JSON 和 JSON 轻型这类格式比 ATOM 或 XML 更高效，并且在传输大量数据时的性能更佳。 下表提供来自示例测试的结果。 可以看到，从 ATOM 切换至 JSON 后，性能提高 30-53%，从 ATOM 切换至新的 JSON 轻型格式（WCF Data Services 5.1 中提供）后，性能提高 67%。  
  
|||||  
|-|-|-|-|  
|行|ATOM|JSON|JSON（轻型）|  
|10000|113 秒|74 秒|68 秒|  
|1000000|1110 秒|853 秒|665 秒|  
  
> [!NOTE]  
>  SSIS OData 源使用 5.6.1 来分析 OData V3 源，并使用 ODataLib 6.12.0 来分析 OData V4 源。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [教程：使用 OData 源](../../integration-services/data-flow/tutorial-using-the-odata-source.md)  
  
-   [在运行时修改 OData 源查询](../../integration-services/data-flow/modify-odata-source-query-at-runtime.md)  
  
-   [OData 源编辑器（“连接”页）](../../integration-services/data-flow/odata-source-editor-connection-page.md)  
  
-   [OData 源编辑器（“列”页）](../../integration-services/data-flow/odata-source-editor-columns-page.md)  
  
-   [OData 源编辑器（“错误输出”页）](../../integration-services/data-flow/odata-source-editor-error-output-page.md)  
  
-   [OData 源属性](../../integration-services/data-flow/odata-source-properties.md)  
  
## <a name="see-also"></a>另请参阅  
 [OData 连接管理器](../../integration-services/connection-manager/odata-connection-manager.md)  
  
  