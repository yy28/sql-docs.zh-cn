---
title: "在没有连接到 Internet 的情况下安装 R 组件 | Microsoft Docs"
ms.custom: ""
ms.date: "02/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0a90c438-d78b-47be-ac05-479de64378b2
caps.latest.revision: 30
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 21
---
# 在没有连接到 Internet 的情况下安装 R 组件
  若要安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 使用的 R 组件，必须连接到 Internet，才能有权访问 Microsoft 下载中心或受信任的站点上的文件。 不过，你可以在没有连接到 Internet 的情况下在服务器上安装这些组件，具体方法为创建本地副本（如本主题中所述）。  
  
  > [!TIP]
  > 
  > 有关脱机安装过程的详细演练，请参阅由[SQL Server 客户顾问团队](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/)发布的此博客
  
## <a name="installation-on-computers-with-no-internet-access"></a>在没有连接到 Internet 的情况下在计算机上安装  
 如果执行脱机安装，[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 将无法访问用于安装必需 R 组件的链接。 若要避免此问题，可以将安装程序的副本下载到本地，并按此处所述的步骤完成安装。
 
 请注意，R 组件有两个安装程序：一个用于 Microsoft R Open，另一个用于 Microsoft R Server。 必须同时下载并安装这两个程序，才能使用 SQL Server R Services。 使用 SQL Server 安装向导可以确保按正确的顺序安装它们。


发行版本  |下载链接  
---------|---------
**SQL Server 2016 RTM**     |           
Microsoft R Open     |[SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266)     
Microsoft R Server     |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051)      
**SQL Server 2016 CU 1**     |           
Microsoft R Open     |[SRO_3.2.2.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808803)     
Microsoft R Server     |[SRS_8.0.3.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808805)      
**SQL Server 2016 CU 2**     |           
Microsoft R Open     |[SRO_3.2.2.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827398)     
Microsoft R Server     |[SRS_8.0.3.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827399)  
**SQL Server 2016 CU 3**     |           
Microsoft R Open     |[SRO_3.2.2.13000_1033.cab: ](https://go.microsoft.com/fwlink/?LinkId=831785)     
Microsoft R Server     |[SRS_8.0.3.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831676)  |
**SQL Server 2016 SP 1**     |           
Microsoft R Open     |[SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879)     
Microsoft R Server     |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881)  
**SQL Server 2016 SP 1 GDR**     |           
Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)     
Microsoft R Server     |[SRS_8.0.3.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)  

  
**如何在脱机安装中更新 R 组件**     

1. 使用以上链接下载适当的版本。
2. 将 CAB 文件复制到要安装更新的计算机上的文件夹中。
3. 运行 SQL Server 安装向导时，请单击 Microsoft R 授权页上的“接受”。  将出现一个对话框，其中列出了下载链接。 输入已下载文件的位置路径。 
4. 单击“下一步”以指示组件可用，并完成 SQL Server 安装向导。
5. 也可以针对开放源代码组件下载存档源代码。 有关详细信息，请参阅[安装 SQL Server R Services](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)。


> [!IMPORTANT] 在连接了 Internet 的计算机上，如果在安装 SQL Server 的过程中下载了 cab 文件，安装向导会检测本地语言并自动更改安装程序的语言。 
> 
> 但是，如果在未连接 Internet 的计算机上安装某个本地化版本的 SQL Server，并且将 R 安装程序下载到本地共享，则必须手动编辑所下载文件的名称，并为正在安装的语言插入正确的语言标识符。 
> 
> 例如，如果安装日语版 SQL Server，应将文件名称从 SRS_8.0.3.0_1033.cab 更改为 SRS_8.0.3.0_1041.cab。    
 
  
## <a name="see-also"></a>另请参阅  
 [SQL Server R Services 入门](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)   
 [R Services 安装问题疑难解答](../Topic/Troubleshooting%20R%20Services%20Setup.md)  
  
  