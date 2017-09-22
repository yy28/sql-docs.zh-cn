---
title: "安装 Analysis Services |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 04/11/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cd6ac80d-b735-4e3e-a024-489f1409ad33
caps.latest.revision: 20
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: cf762b3aaeb222e456b0b46256a7d7f0efddbf48
ms.contentlocale: zh-cn
ms.lasthandoff: 09/21/2017

---
# <a name="install-sql-server-analysis-services"></a>安装 SQL Server Analysis Services
  SQL Server Analysis Services 是托管表格模型、多维数据集以及数据挖掘模型的分析数据库服务器，可从报表、电子表格和仪表板进行访问。  
  
 Analysis Services 是多实例，这意味着你可以在一台计算机上安装多个副本或运行新和旧版本并行。 安装的任何示例都以三种模式之一运行，这是在安装期间确定的：多维和数据挖掘、表格或 SharePoint。 如果你想使用多种模式，每种模式都将需要一个单独实例。  
  
 在某种模式下安装了服务器后，可以用它来托管符合该模式的解决方案。 例如，如果你想通过网络来访问表格模型数据，则需要表格模式服务器。  
  
## <a name="get-tools-and-designers"></a>获取工具和设计器  
 SQL Server 安装程序不再安装模型设计器或用于解决方案设计或服务器管理的管理工具。 在此版本中，工具都是独立安装的，你可以从以下获得这些工具：  
  
-   [下载 SQL Server Management Studio (SSMS)](/sql-docs/docs/ssms/download-sql-server-management-studio-ssms)  
  
-   [下载 SQL Server Data Tools (SSDT)](/sql-docs/docs/ssdt/download-sql-server-data-tools-ssdt)  
  
 需同时具备 SSMS 和 SSDT，才可使用 Analysis Services 实例和数据。 可将工具安装在任何位置，但请确保先在服务器上配置端口，再尝试连接。 有关详细信息，请参阅 [Configure the Windows Firewall to Allow Analysis Services Access](../../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md) 。  
  
## <a name="install-using-a-wizard"></a>使用向导进行安装  
 下面的列表显示了 SQL Server 安装向导中的哪些页用于安装 Analysis Services。  
  
1.  从安装程序的功能树中选择 **“Analysis Services”** 。  
  
     ![安装程序功能树显示 Analsyis 服务](../../../analysis-services/instances/install-windows/media/ssas-setupas.gif "显示 Analsyis 服务的安装程序功能树")  
  
2.  在“Analysis Services 配置”页上，选择一种模式。 表格模式下是默认设置...  
  
     ![使用 Analysis Services 配置选项的设置页](../../../analysis-services/instances/install-windows/media/ssas-setupasconfig.png "使用 Analysis Services 配置选项的设置页")  
  
  表格模式使用 xVelocity 内存中分析引擎 (VertiPaq)，该引擎是表格模型的默认存储器。 将表格模型部署到服务器之后，可选择性地配置表格解决方案，以便使用 DirectQuery 磁盘存储代替受内存限制的存储。  
 
 多维和数据挖掘模式使用 MOLAP 作为部署到 Analysis Services 的模型的默认存储。 在部署到服务器之后，如果你想直接对关系数据库允许查询而不是将查询数据存储在 Analysis Services 多维数据库中，你可以配置解决方案以使用 ROLAP。  
  

  
 在使用非默认的存储模式时，可以调整内存管理和 IO 设置以获得更好的性能。 有关详细信息，请参阅 [Analysis Services 中的服务器属性](../../../analysis-services/server-properties/server-properties-in-analysis-services.md) 。  
  
## <a name="command-line-setup"></a>命令行安装程序  
 SQL Server 安装程序包含指定服务器模式的参数 (**ASSERVERMODE**)。 下面的示例说明了用来在表格服务器模式下安装 Analysis Services 的命令行安装程序。  
  
```  
  
Setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=install /FEATURES=AS /ASSERVERMODE=TABULAR /INSTANCENAME=ASTabular /INDICATEPROGRESS/ASSVCACCOUNT=<DomainName\UserName> /ASSVCPASSWORD=<StrongPassword> /ASSYSADMINACCOUNTS=<DomainName\UserName>   
```  
  
 **INSTANCENAME** 必须少于 17 个字符。  
  
 所有占位符帐户的值必须替换为有效的帐户和密码。  
  
 **ASSERVERMODE** 区分大小写。  所有值必须以大写形式表示。 下表对 **ASSERVERMODE**的有效值进行了说明。  
  
|值|说明|  
|-----------|-----------------|  
|TABULAR|这是默认值。 如果你未设置**ASSERVERMODE**，在表格模式下安装了服务器。|
|MULTIDIMENSIONAL|该值是可选的。|  
|POWERPIVOT|该值是可选的。 实际上，如果设置 **ROLE** 参数，会自动将服务器模式设置为 1，从而使 **ASSERVERMODE** 成为 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 安装的可选项。 有关详细信息，请参阅 [从命令提示符安装 Power Pivot](http://msdn.microsoft.com/en-us/7f1f2b28-c9f5-49ad-934b-02f2fa6b9328)。|  
  
  
## <a name="see-also"></a>另请参阅  
 [确定 Analysis Services 实例的服务器模式](../../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)   
 [表格建模 (SSAS 表格)](https://msdn.microsoft.com/library/hh212945(v=sql.110).aspx)  
  
  

