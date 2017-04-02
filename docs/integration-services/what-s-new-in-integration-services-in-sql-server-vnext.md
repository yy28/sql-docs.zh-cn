---
title: "SQL Server vNext Integration Services 中的新增功能 | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e26d7884-e772-46fa-bfdc-38567fe976a1
caps.latest.revision: 4
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 3
---
# SQL Server vNext Integration Services 中的新增功能
本主题介绍 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中新增或更新的功能。

>   [!NOTE] SQL Server vNext 还包括 SQL Server 2016 的功能以及 SQL Server 2016 更新中新增的功能。 若要了解 SQL Server 2016 中的新 SSIS 功能，请参阅[SQL Server 2016 Integration Services 中的新增功能](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)。

## <a name="new-in-ssis-in-sql-server-vnext-ctp-11"></a>SQL Server vNext CTP 1.1 中的新 SSIS 功能

SQL Server vNext CTP 1.1 不提供新的 SSIS 功能。

## <a name="new-in-ssis-in-sql-server-vnext-ctp-10"></a>SQL Server vNext CTP 1.0 中的新 SSIS 功能

### <a name="scale-out-for-ssis"></a>SSIS 的 Scale Out

Scale Out 功能使在多台计算机上运行 [!INCLUDE[ssIS_md](../includes/ssis-md.md)] 变得更加简单。 
   
安装 Scale Out Master 和 Worker 之后，可分发包以在不同的 Worker 上自动执行。 如果执行意外终止，将自动重试该执行。 此外，可使用 Master 集中管理所有执行和 Worker。
   
有关详细信息，请参阅 [Integration Services Scale Out](../integration-services/integration-services-ssis-scale-out.md)。
   
### <a name="support-for-microsoft-dynamics-online-resources"></a>支持 Microsoft Dynamics Online 资源

OData 源和 OData 连接管理器现支持连接到 Microsoft Dynamics AX Online 和 Microsoft Dynamics CRM Online 的 OData 源。
