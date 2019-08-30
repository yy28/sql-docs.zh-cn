---
title: SQL Server Azure 中的数据文件 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
ms.assetid: 38ffd9c2-18a5-43d2-b674-e425addec4e4
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 55f0ab0cf2f1d4a29c0fca252c45f9e92740851c
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2019
ms.locfileid: "70154542"
---
# <a name="sql-server-data-files-in-azure"></a>SQL Server Azure 中的数据文件
  SQL Server Azure 中的数据文件, 可以对作为 Azure Blob 存储的 SQL Server 数据库文件提供本机支持。 通过此功能, 你可以在本地或 Azure 中的虚拟机上运行的 SQL Server 中创建数据库, 并在 Azure Blob 存储中为数据创建专用存储位置。 此增强功能使用分离和附加操作，简化了计算机之间的数据库移动。 此外, 它还允许从或向 Azure 存储还原, 为数据库备份文件提供备用存储位置。 因此，它在数据虚拟化、数据移动、安全性和可用性、轻松降低成本以及维护方面都具备优势，可实现高可用性和弹性扩展，支持几种混合解决方案。  
  
 本主题介绍在 Azure 存储服务中存储 SQL Server 数据文件的核心概念和注意事项。  
  
 有关如何使用此新功能的实践体验，请参阅[教程：SQL Server Azure 存储服务](../tutorial-use-azure-blob-storage-service-with-sql-server-2016.md)中的数据文件。  
  
 下图演示了此增强功能使你能够将 SQL Server 数据库文件存储为 Azure 存储中的 Azure blob, 而不管服务器驻留在何处。  
  
 ![SQL Server 与 Azure 存储集成](../../database-engine/media/sql-server-dbfiles-stored-as-blobs.gif "SQL Server 与 Azure 存储集成")  
  
## <a name="benefits-of-using-sql-server-data-files-in-azure"></a>在 Azure 中使用 SQL Server 数据文件的好处  
  
-   **迁移方便快捷优势：** 此功能在本地计算机之间以及在本地与云环境中的计算机之间一次迁移一个数据库，从而简化了迁移过程，而无需进行任何应用程序更改。 因此，它能在保持现有本地基础架构不变的情况下支持增量迁移。 此外，在应用程序需要在本地环境多个位置运行时，对集中数据存储的访问权限可以简化应用程序逻辑。 在某些情况下，可能需要在地理上分散的位置快速设置计算机中心，以便从很多不同来源收集数据。 通过使用这项新的增强功能, 你可以将多个数据库存储为 Azure blob, 然后运行 Transact-sql 脚本在本地计算机或虚拟机上创建数据库, 而不是将数据从一个位置移动到另一个位置。  
  
-   **成本和无限制存储优势：** 利用此功能, 你可以在 Azure 中使用无限制的站外存储, 同时利用本地计算资源。 当你使用 Azure 作为存储位置时, 可以轻松地将精力集中在应用程序逻辑上, 而不会产生硬件管理开销。 如果丢失一个本地计算节点，无需进行任何数据移动操作即可设置新节点。  
  
-   **高可用性和灾难恢复优势：** 使用 Azure 中的 SQL Server 数据文件可简化高可用性和灾难恢复解决方案。 例如, 如果 Azure 中的虚拟机或 SQL Server 的实例发生故障, 则可以通过只重新建立指向 Azure Blob 的链接, 在新计算机中重新创建数据库。  
  
-   **安全性优势：** 通过此新增强功能可将计算实例与存储实例分离。 您可以仅在计算实例而不在存储实例中对完全加密的数据库进行解密。 换句话说，使用此新增强功能，您可以使用透明数据加密 (TDE) 证书（此证书与数据在物理上是分离的）来加密在公共云中的所有数据。 TDE 密钥可存储在主数据库中，该数据库存储在物理上安全的本地计算机中，并在本地备份。 你可以使用这些本地密钥来加密驻留在 Azure 存储中的数据。 即使您的云存储帐户凭据被盗，数据仍然安全，因为 TDE 证书始终驻留在本地。  
  
## <a name="concepts-and-requirements"></a>概念和要求  
  
### <a name="azure-storage-concepts"></a>Azure 存储概念  
 使用 Azure 功能中的 SQL Server 数据文件时, 需要在 Azure 中创建存储帐户和容器。 然后，需要创建一个 SQL Server 凭据，其中包括有关容器策略的信息以及访问容器所需的共享访问签名。  
  
 在 Azure 中, 存储帐户表示用于访问 Blob 的最高级别的命名空间。 一个存储帐户可含有无限数量的容器，前提是总大小在 500 TB 以内。 有关存储限制的最新信息，请参阅 [Azure 订阅与服务限制、配额和约束](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/)。 容器提供一组 Blob 集。 所有 Blob 必须都在一个容器中。 一个帐户可以包含无限数量的容器。 同样，一个容器可以存储无限数量的 Blob。 Azure 存储中可存储两类 Blob：块 Blob 和页 Blob。 这一新功能使用页 Blob，页 Blob 最大可到 1 TB，当文件字节数经常修改时更为高效。 你可以使用以下 URL 格式访问 Blob： `http://storageaccount.blob.core.windows.net/<container>/<blob>`。  
  
### <a name="azure-billing-considerations"></a>Azure 计费注意事项  
 在决策制定和规划过程中，估计使用 Azure 服务的成本是一项非常重要的工作。 在 Azure 存储中存储 SQL Server 数据文件时，需要支付与存储和事务相关的成本。 此外，要实现“Azure 存储中的 SQL Server 数据文件”功能，需要每 45 到 60 秒隐式进行一次 Blob 续租。 这也会对每个数据库文件（如 .mdf 或 .ldf）造成事务成本。 根据我们的估计，基于当前定价模型，两个数据库文件（.mdf 和 .ldf）的续租成本大约为每个月 2 美分。 建议使用 [Azure 定价](https://azure.microsoft.com/pricing/) 页面上的信息来帮助估计每月与使用 Azure 存储和 Azure 虚拟机相关的成本。  
  
### <a name="sql-server-concepts"></a>SQL 服务器概念  
 使用此新增强功能时，需要执行以下操作：  
  
-   必须创建容器策略并生成共享访问签名 (SAS) 密钥。  
  
-   对于数据或日志文件使用的每个容器，都必须创建名称与容器路径匹配的 SQL Server 凭据。  
  
-   必须在 SQL Server 凭据存储中存储有关 Azure 存储容器、其关联策略名称以及 SAS 密钥的信息。  
  
 下面的示例假定已创建了一个 Azure 存储容器, 并且已创建了具有读取、写入、列出权限的策略。 创建容器策略会生成一个 SAS 密钥，它以未加密状态安全存储在内存中，SQL Server 需要使用它来访问容器中的 Blob 文件。 在下面的代码段中，将 `'your SAS key'` 替换为类似于以下内容的项： `'sr=c&si=<MYPOLICYNAME>&sig=<THESHAREDACCESSSIGNATURE>'`。 有关详细信息, 请参阅[创建和使用共享访问签名](https://msdn.microsoft.com/library/azure/jj721951.aspx)  
  
```  
  
-- Create a credential  
CREATE CREDENTIAL [https://testdb.blob.core.windows.net/data]  
WITH IDENTITY='SHARED ACCESS SIGNATURE',  
SECRET = 'your SAS key'  
  
-- Create database with data and log files in Azure container.  
CREATE DATABASE testdb   
ON  
( NAME = testdb_dat,  
    FILENAME = 'https://testdb.blob.core.windows.net/data/TestData.mdf' )  
 LOG ON  
( NAME = testdb_log,  
    FILENAME =  'https://testdb.blob.core.windows.net/data/TestLog.ldf')  
  
```  
  
 **重要说明：** 如果当前存在任何对容器中数据文件的引用，则尝试删除相应的 SQL Server 凭据会失败。  
  
### <a name="security"></a>安全性  
 以下是在 Azure 存储中存储 SQL Server 数据文件时的安全注意事项和要求。  
  
-   为 Azure Blob 存储服务创建容器时，建议将访问权限设置为“私有”。 将访问权限设置为“私有”后，只有 Azure 帐户所有者才可读取容器和 Blob 数据。  
  
-   在 Azure 存储中存储 SQL Server 数据库文件时，需要使用共享访问签名，它是授予对容器、Blob、队列和表的受限访问权限的 URI。 通过使用共享访问签名，可以让 SQL Server 在不共享 Azure 存储帐户密钥的情况下访问存储帐户中的资源。  
  
-   此外，建议对数据库继续实施传统的本地安全做法。  
  
### <a name="installation-prerequisites"></a>安装必备组件  
 下面是在 Azure 中存储 SQL Server 数据文件时的安装先决条件。  
  
-   **本地 SQL Server：** SQL Server 2014 版本包括此功能。 要了解如何下载 SQL Server 2014，请参阅 [SQL Server 2014](https://www.microsoft.com/sqlserver/sql-server-2014.aspx)。  
  
-   在 Azure 虚拟机中运行 SQL Server:如果要在 Azure 虚拟机上安装 SQL Server, 请安装 SQL Server 2014, 或更新现有实例。 同样, 还可以使用 SQL Server 2014 平台映像在 Azure 中创建新的虚拟机。 要了解如何下载 SQL Server 2014，请参阅 [SQL Server 2014](https://www.microsoft.com/sqlserver/sql-server-2014.aspx)。  
  
###  <a name="bkmk_Limitations"></a> 限制  
  
-   在此功能的当前版本中, 不`FileStream`支持在 Azure 存储中存储数据。 你可以在`Filestream` azure 存储集成的本地数据库中存储数据, 但不能使用 azure 存储在计算机之间移动 Filestream 数据。 对于 `FileStream` 数据，建议继续使用传统方法在不同计算机之间移动与 Filestream 关联的文件（.mdf，.ldf）。  
  
-   目前，此新增强功能不支持多个 SQL Server 实例同时访问 Azure 存储中的相同数据库文件。 如果 ServerA 处于联机状态并且包含一个活动数据库文件，ServerB 意外启动并且也包含一个指向相同数据文件的数据库，则第二个服务器将无法启动该数据库，错误代码为 **5120 无法打开物理文件 "%.\*ls"。操作系统错误 %d：“%ls”** 。  
  
-   只有 .mdf、.ldf 和 .ndf 文件才可以通过使用 Azure 功能中的 SQL Server 数据文件存储在 Azure 存储中。  
  
-   使用“Azure 中的 SQL Server 数据文件”功能时，存储帐户不支持异地复制。 如果对存储帐户进行地理复制并发生地理故障转移，则可能出现数据库损坏。  
  
-   每个 Blob 最大可为 1 TB。 这就对可存储在 Azure 存储中的单个数据库的数据和日志文件设定了一个上限。  
  
-   无法使用“Azure 存储中的 SQL Server 数据文件”功能在 Azure Blob 中存储内存 OLTP 数据。 这是因为内存中 OLTP 依赖于`FileStream`和, 在此功能的当前版本中, 不支持在 Azure 存储中存储`FileStream`数据。  
  
-   使用 Azure 功能中的 SQL Server 数据文件时, SQL Server 使用`master`数据库中的排序规则集执行所有 URL 或文件路径比较。  
  
-   只要不在主数据库中添加新数据库文件，就支持 `AlwaysOn Availability Groups`。 如果某个数据库操作需要在主数据库中创建新文件，请首先在辅助节点上禁用 AlwaysOn 可用性组。 然后对主数据库执行该数据库操作，并在主节点中备份该数据库。 接下来，将数据库还原到辅助节点，并在辅助节点上启用 AlwaysOn 可用性组。 请注意, 使用 Azure 功能中的 SQL Server 数据文件时, 不支持 AlwaysOn 故障转移群集实例。  
  
-   在正常操作期间，SQL Server 使用临时租约来保留用于存储的 Blob，并且每 45 到 60 秒续租每个 Blob。 如果服务器崩溃，启动另一个配置为使用相同 Blob 的 SQL Server 实例，则新实例将等待 60 秒，以待现有 Blob 租约过期。 如果要将数据库附加到另一个实例，又无法在 60 秒内等待租约过期，则可显式中断 Blob 租约，以免执行附加操作时发生任何故障。  
  
## <a name="tools-and-programming-reference-support"></a>工具和编程参考支持  
 本节介绍在 Azure 存储中存储 SQL Server 数据文件时可使用的工具和编程参考库。  
  
### <a name="powershell-support"></a>PowerShell 支持  
 在 SQL Server 2014 中, 通过引用 Blob 存储 URL 路径而不是文件路径, 可以使用 PowerShell cmdlet 将 SQL Server 的数据文件存储在 Azure Blob 存储服务中。 您可以使用以下 URL 格式访问 Blob`: http://storageaccount.blob.core.windows.net/<container>/<blob>` 。  
  
### <a name="sql-server-object-and-performance-counters-support"></a>SQL Server 对象和性能计数器支持  
 从 SQL Server 2014 起，增加了一个与“Azure 存储中的 SQL Server 数据文件”功能结合使用的新 SQL Server 对象。 新的 SQL Server 对象称为[SQL Server, HTTP_STORAGE_OBJECT,](../performance-monitor/sql-server-http-storage-object.md)系统监视器可使用它在使用 Azure 存储运行 SQL Server 时监视活动。  
  
### <a name="sql-server-management-studio-support"></a>SQL Server Management Studio 支持  
 使用 SQL Server Management Studio 时，您可通过多个对话框窗口使用此功能。 例如，您可以在几个对话框窗口（如“新建数据库” `https://teststorageaccnt.blob.core.windows.net/testcontainer/` 、 **“附加数据库”** 和 **“还原数据库”** ）中的 **“路径”** 中键入存储容器的 URL 路径（如）。 有关详细信息，请参阅[教程：SQL Server Azure 存储服务](../tutorial-use-azure-blob-storage-service-with-sql-server-2016.md)中的数据文件。  
  
### <a name="sql-server-management-objects-support"></a>SQL Server 管理对象支持  
 使用“Azure 中的 SQL Server 数据文件”功能时，支持所有 SQL Server 管理对象 (SMO)。 如果 SMO 对象需要文件路径，请使用 BLOB URL 格式而不是本地文件路径，如 `https://teststorageaccnt.blob.core.windows.net/testcontainer/`。 有关 SQL Server 管理对象的详细信息，请参阅 SQL Server 联机丛书中的 [SQL Server 管理对象 (SMO) 编程指南](../server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)。  
  
### <a name="transact-sql-support"></a>Transact-SQL 支持  
 此新功能在 Transact-SQL 外围应用中引入了以下更改：  
  
-   **sys.master_files** 系统视图中新增一个 **int**列，即 **credential_id** 。 **credential_id** 列用于实现将支持 Azure 存储的数据文件交叉引用回为其创建的凭据的 sys.credentials。 您可以使用它来排除故障，如当有数据库文件使用凭据时无法删除凭据。  
  
##  <a name="bkmk_Troubleshooting"></a>排查 Azure 中的 SQL Server 数据文件问题  
 为避免不受支持的功能或限制造成的错误，首先请查看 [Limitations](sql-server-data-files-in-microsoft-azure.md#bkmk_Limitations)。  
  
 下面列出了使用“Azure 存储中的 SQL Server 数据文件”功能时可能遇到的错误。  
  
 **身份验证错误**  
  
-   *凭据 '%.\*ls' 被某活动数据库文件使用，因此无法删除它。*    
    解决方法：尝试删除 Azure 存储中活动数据库文件仍在使用的凭据时，可能会看到此错误。 要删除凭据，必须先删除拥有此数据库文件的关联 Blob。 要删除具有活动租约的 Blob，必须先中断租约。  
  
-   *未在容器上正确创建共享访问签名。*    
     解决方法：确保已在容器上正确创建了共享访问签名。 有关第 2 课中提供的说明，请参阅[教程：SQL Server Azure 存储服务](../tutorial-use-azure-blob-storage-service-with-sql-server-2016.md)中的数据文件。  
  
-   *尚未正确创建 SQL Server 凭据。*    
    解决方法：确保已对“标识”字段使用了“共享访问签名”，并正确创建了机密。 有关第 3 课中提供的说明，请参阅[教程：SQL Server Azure 存储服务](../tutorial-use-azure-blob-storage-service-with-sql-server-2016.md)中的数据文件。  
  
 **租赁 Blob 错误：**  
  
-   在使用相同 Blob 文件的 SQL Server 实例崩溃之后，尝试启动另一个 SQL Server 时发生错误。 解决方法：在正常操作期间，SQL Server 使用临时租约来保留用于存储的 Blob，并且每 45 到 60 秒续租每个 Blob。 如果服务器崩溃，启动另一个配置为使用相同 Blob 的 SQL Server 实例，则新实例将等待 60 秒，以待现有 Blob 租约过期。 如果要将数据库附加到另一个实例，又无法在 60 秒内等待租约过期，则可显式中断 Blob 租约，以免执行附加操作时发生任何故障。  
  
 **数据库错误**  
  
1.  *创建数据库时出错*   
    解决方法：有关第 4 课中提供的说明，请参阅[教程：SQL Server Azure 存储服务](../tutorial-use-azure-blob-storage-service-with-sql-server-2016.md)中的数据文件。  
  
2.  *运行 Alter 语句时出错*   
    解决方法：确保在数据库联机时执行 Alter Database 语句。 将数据文件复制到 Azure 存储时，始终创建页 Blob 而不是块 Blob。 否则，ALTER Database 将失败。 有关第 7 课中提供的说明，请参阅[教程：SQL Server Azure 存储服务](../tutorial-use-azure-blob-storage-service-with-sql-server-2016.md)中的数据文件。  
  
3.  *错误代码 5120 无法打开物理文件“%.\*ls”。操作系统错误 %d:“%ls”*    
    解决方法：目前，此新增强功能不支持多个 SQL Server 实例同时访问 Azure 存储中的相同数据库文件。 如果 ServerA 处于联机状态并且包含一个活动数据库文件，ServerB 意外启动并且也包含一个指向相同数据文件的数据库，则第二个服务器将无法启动该数据库，错误代码为 *5120 无法打开物理文件 "%.\*ls".操作系统错误 %d：“%ls”* 。  
  
     要解决此问题，首先需要确定是否需要 ServerA 访问 Azure 存储中的数据库文件。 如果不需要，只需删除 ServerA 与 Azure 存储中数据库文件之间的任何连接。 为此，请按照下列步骤进行操作：  
  
    1.  使用 ALTER Database 语句将 ServerA 的文件路径设置为本地文件夹。  
  
    2.  在 ServerA 中将数据库设置为脱机状态。  
  
    3.  然后，将数据库文件从 Azure 存储复制到 Server A 中的本地文件夹。这可确保 ServerA 仍有一个本地数据库副本。  
  
    4.  将数据库设置为联机状态。  
  
## <a name="see-also"></a>请参阅  
 [教程：SQL Server Azure 存储服务中的数据文件](../tutorial-use-azure-blob-storage-service-with-sql-server-2016.md)  
  
  
