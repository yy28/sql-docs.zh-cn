---
title: 升级 Data Quality Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: f396666b-7754-4efc-9507-0fd114cc32d5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5c76fda112acae7b8a9314d217f5c32d197e87f9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62775627"
---
# <a name="upgrade-data-quality-services"></a>升级 Data Quality Services
  本主题的信息介绍如何将现有 Data Quality Services (DQS) 安装升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP2。 在将 DQS 中的数据质量服务器升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]时，您还必须升级 DQS 数据库架构。  
  
> [!IMPORTANT]
>  -   您必须先备份 DQS 数据库，然后才能升级 DQS，以防止在架构升级过程中出现任何意外数据损失。 有关备份 DQS 数据库的信息，请参阅 [Backing Up and Restoring DQS Databases](../../data-quality-services/backing-up-and-restoring-dqs-databases.md)。  
> -   通过使用当前或早期版本的数据质量客户端或 Integration Services 中的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] DQS 清除转换 [，你可以连接](../../integration-services/data-flow/transformations/dqs-cleansing-transformation.md) 版数据质量服务器，执行你的数据质量任务。  
> -   在将 Data Quality Services 和 Master Data Services 升级到 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] CTP2 后，您可以使用用于 Excel 的 Master Data Services 外接程序的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] SP1 版本继续进行。 但是，在升级到 SQL Server 2014 CTP2 后，用于 Excel 的 Master Data Services 外接程序的任何早期版本都无法使用。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 您可以从 [此处](https://go.microsoft.com/fwlink/?LinkId=328664)下载用于 Excel 的 Master Data Services 外接程序的  SP1 版本。  
  
##  <a name="Prerequisites"></a> 先决条件  
  
-   您必须作为 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 计算机上 Administrators 组的成员登录。  
  
-   您的 Windows 用户帐户必须是安装了 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 的 SQL Server 实例中 sysadmin 固定服务器角色的成员。  
  
##  <a name="Upgrade"></a> 升级 DQS  
 要升级 DQS：  
  
1.  首先备份 DQS 数据库，然后再启动升级过程。 有关备份 DQS 数据库的信息，请参阅 [Backing Up and Restoring DQS Databases](../../data-quality-services/backing-up-and-restoring-dqs-databases.md)。  
  
2.  将安装 DQS 的 SQL 实例升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
    1.  运行 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装向导。  
  
    2.  在左窗格中，单击 **“安装”**。  
  
    3.  在右窗格中，单击**从 SQL Server 2005 中，SQL Server 2008、 SQL Server 2008 R2 或 SQL Server 2012 升级**。  
  
    4.  完成安装向导。  
  
        > [!NOTE]  
        >  这会将您的 SQL Server 实例升级为 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ，而且如果此计算机以前安装过数据质量客户端，还会安装最新的数据质量客户端。 如果您在其他计算机上安装了数据质量客户端，您必须在那些计算机上运行步骤 2 的这些分步骤，安装最新版的数据质量客户端。 安装向导会安装与现有的数据质量客户端并存的当前版本数据质量客户端。 升级完 DQS 数据架构后，通过使用当前或早期版本的数据质量客户端，您可以连接 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版数据质量服务器。  
  
3.  升级 DQS 数据库架构。  
  
    1.  作为管理员启动命令提示符。  
  
    2.  在命令提示符下，将目录更改为 DQSInstaller.exe 出现的位置。 对于 SQL Server 的默认实例，DQSInstaller.exe 文件将出现在 C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn 下：  
  
        ```  
        cd C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn  
        ```  
  
    3.  在命令提示符下，键入以下命令，再按 Enter：  
  
        ```  
        dqsinstaller.exe -upgrade  
        ```  
  
    4.  安装程序会提示您在继续操作之前备份 DQS 数据库。 如果已经备份 DQS 数据库，请键入 `Y` 或 `Yes`，然后按 Enter 以继续升级。  
  
    5.  在成功升级 DQS 数据库架构之后，将显示一条完成消息。  
  
##  <a name="Verify"></a> 验证 DQS 数据库架构升级  
 要验证是否成功升级了 DQS 数据库架构，您可以查询每个数据库中的 A_DB_VERSION 表来检查 DQS_MAIN 和 DQS_PROJECTS 数据库中的当前版本。 为此，请执行以下操作：  
  
1.  启动 SQL Server Management Studio 并连接到包含升级的 DQS 数据库架构的 SQL Server 实例。  
  
2.  运行以下查询：  
  
    ```  
    SELECT * FROM DQS_MAIN.dbo.A_DB_VERSION WHERE STATUS=2;  
    SELECT * FROM DQS_PROJECTS.dbo.A_DB_VERSION WHERE STATUS=2;  
    ```  
  
3.  输出将为每个升级显示一条信息，并显示升级的日期。 最新日期的最大 VERSION_ID 和 ASSEMBLY_VERSION 是当前版本。 STATUS 列中的值为 2 时指示成功。 如果发生错误，错误将在 ERROR 列中列出。 示例输出：  
  
    |ID|UPGRADE_DATE|VERSION_ID|ASSEMBLY_VERSION|USER_NAME|STATUS|error|  
    |--------|-------------------|-----------------|-----------------------|----------------|------------|-----------|  
    |1000|2013-08-11 05:26:39.567|1200|11.0.3000.0|\<DOMAIN\UserName>|2||  
    |1001|2013-09-19 15:09:37.750|1600|12.0.xxxx.0|\<DOMAIN\UserName>|2||  
  
## <a name="see-also"></a>请参阅  
 [安装 Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)   
 [删除 Data Quality Server 对象](../../sql-server/install/remove-data-quality-server-objects.md)   
 [升级到 SQL Server 2014](upgrade-sql-server.md)  
  
  
