---
title: 分离和附加 DQS 数据库 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 830e33bc-dd15-4f8e-a4ac-d8634b78fe45
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: e10cc69f3fe32656418a8714c852d86e631fe281
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56024388"
---
# <a name="detaching-and-attaching-dqs-databases"></a>分离数据库和附加 DQS 数据库

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  本主题介绍如何分离和附加 DQS 数据库。  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Limitations"></a> 限制和局限  
 有关限制和局限的列表，请参阅 [数据库分离和附加 (SQL Server)](../relational-databases/databases/database-detach-and-attach-sql-server.md)中分离数据库。  
  
###  <a name="Prerequisites"></a> 先决条件  
  
-   确保 DQS 中没有正在运行的活动或过程。 这可以使用 **“活动监视”** 屏幕进行验证。 有关使用该屏幕的详细信息，请参阅 [Monitor DQS Activities](../data-quality-services/monitor-dqs-activities.md)。  
  
-   确保没有用户已登录 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
  
-   您的 Windows 用户帐户必须是 SQL Server 实例中 db_owner 固定服务器角色的成员，才能分离 DQS 数据库。  
  
-   您的 Windows 用户帐户必须具有 CREATE DATABASE、CREATE ANY DATABASE 或 ALTER ANY DATABASE 权限，才能附加数据库。  
  
-   您必须具有 DQS_MAIN 数据库的 dqs_administrator 角色，才能终止 DQS 中任何正在运行的活动或停止任何正在运行的过程。  
  
##  <a name="Detach"></a> 分离 DQS 数据库  
 在您使用 SQL Server Management Studio 分离 DQS 数据库时，分离后的文件将保留在您的计算机上，并且可以重新附加到同一个 SQL Server 实例上，也可以移到其他服务器上并附加其上。 DQS 数据库文件通常位于 Data Quality Services 计算机上的以下位置：C:\Program Files\Microsoft SQL Server\MSSQL13.<Instance_Name>\MSSQL\DATA。  
  
1.  启动 Microsoft SQL Server Management Studio 并连接到适当的 SQL Server 实例。  
  
2.  在“对象资源管理器”中，展开 **“数据库”** 节点。  
  
3.  右键单击 **DQS_MAIN** 数据库，指向 **“任务”**，再单击 **“分离”**。 将出现 **“分离数据库”** 对话框。  
  
4.  选中 **“删除”** 列下的复选框，然后单击 **“确定”** 以便分离 DQS_MAIN 数据库。  
  
5.  对 DQS_PROJECTS 和 DQS_STAGING_DATA 数据库重复执行步骤 3 和步骤 4，以便分离它们。  
  
 您还可以使用 sp_detach_db 存储过程通过 Transact-SQL 语句分离 DQS 数据库。 有关使用 Transact-SQL 语句分离数据库的详细信息，请参阅 [Using Transact-SQL](../relational-databases/databases/detach-a-database.md#TsqlProcedure) 中的 [Detach a Database](../relational-databases/databases/detach-a-database.md)。  
  
##  <a name="Attach"></a> 附加 DQS 数据库  
 使用以下说明可以将 DQS 数据库附加到原来从其上分离出来的 SQL Server 实例，或是其他安装了 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 的 SQL Server 实例。  
  
1.  启动 Microsoft SQL Server Management Studio 并连接到适当的 SQL Server 实例。  
  
2.  在对象资源管理器中，右键单击 **“数据库”**，然后单击 **“附加”**。 将出现 **“附加数据库”** 对话框。  
  
3.  若要指定要附加的数据库，请单击 **“添加”**。 **“定位数据库文件”** 对话框将出现。  
  
4.  选择数据库驻留的磁盘驱动器，然后展开目录树以便找到并选择该数据库的 .mdf 文件。 例如，对于 DQS_MAIN 数据库：  
  
    ```  
    C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA\DQS_MAIN.mdf  
    ```  
  
5.  **“数据库详细信息”** （下部）窗格将显示要附加的文件的名称。 若要验证或更改文件的路径名，请单击“浏览”按钮 (…)。  
  
6.  单击 **“确定”** 将附加该 DQS_MAIN 数据库。  
  
7.  对 DQS_PROJECTS 和 DQS_STAGING_DATA 数据库重复执行步骤 2-6，以便附加它们。  
  
8.  在还原 DQS_MAIN 数据库后您还必须在接下来的步骤中运行 Transact-SQL 语句，否则，在您尝试通过使用数据质量客户端应用程序连接到数据质量服务器时系统将会显示错误消息，并且您将无法连接。 但是，如果您只是附加 DQS_PROJECTS 或 DQS_STAGING_DATA 数据库，而不是 DQS_MAIN，则不需要执行步骤 9 和 10。  
  
     若要运行 Transact-SQL 语句，请在对象资源管理器中，右键单击服务器，然后单击 **“新建查询”**。  
  
9. 在“查询编辑器”窗口中，复制以下 SQL 语句：  
  
    ```  
    ALTER DATABASE [DQS_MAIN] SET TRUSTWORTHY ON;  
    EXEC sp_configure 'clr enabled', 1;  
    RECONFIGURE WITH OVERRIDE  
    ALTER DATABASE [DQS_MAIN] SET ENABLE_BROKER  
    ALTER AUTHORIZATION ON DATABASE::[DQS_MAIN] TO [##MS_dqs_db_owner_login##]  
    ALTER AUTHORIZATION ON DATABASE::[DQS_PROJECTS] TO [##MS_dqs_db_owner_login##]  
  
    ```  
  
10. 按 F5 执行这些语句。 查看“结果”窗格以便验证这些语句已成功执行。 您将看到下列消息： `Configuration option 'clr enabled' changed from 1 to 1. Run the RECONFIGURE statement to install.`  
  
11. 使用数据质量客户端连接到数据质量服务器以便验证您是否可以成功连接。  
  
 您还可以使用 Transact-SQL 语句附加 DQS 数据库。 有关使用 Transact-SQL 语句附加数据库的详细信息，请参阅 [Using Transact-SQL](../relational-databases/databases/attach-a-database.md#TsqlProcedure) 中的 [Attach a Database](../relational-databases/databases/attach-a-database.md)。  
  
## <a name="see-also"></a>另请参阅  
 [管理 DQS 数据库](../data-quality-services/manage-dqs-databases.md)  
  
  
