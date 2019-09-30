---
title: 连接到 Azure Blob 存储（SQL Server 导入和导出向导）| Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e2e482b8-5f90-48c5-93fb-b412ed52659f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 17330bafe2655f0569f0828706d5e29ed2af3812
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2019
ms.locfileid: "71285355"
---
# <a name="connect-to-azure-blob-storage-sql-server-import-and-export-wizard"></a>连接到 Azure Blob 存储（SQL Server 导入和导出向导）

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


本主题介绍如何从 SQL Server 导入和导出向导的“选择数据源”或“选择目标”页连接到 Azure Blob 存储数据源    。

> [!NOTE]
> 要使用 Azure Blob 源或目标，必须安装用于 SQL Server Integration Services 的 Azure 功能包。
> - 要下载功能包，请参阅[用于 Azure 的 Microsoft SQL Server 2016 Integration Services 功能包](https://www.microsoft.com/download/details.aspx?id=49492)。
> 
> - 有关详细信息，请参阅[用于 Integration Services 的 Azure 功能包 (SSIS)](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)。

以下屏幕截图显示了配置与 Azure Blob 存储的连接的选项。

![Azure Blob 存储 连接](../../integration-services/import-export-data/media/azure-blob-storage-connection.png)

## <a name="options-to-specify"></a>要指定的选项

> [!NOTE]
> 无论 Azure Blob 存储是源还是目标，此数据提供程序的连接选项都相同。 也就是说，在向导的“选择数据源”页和“选择目标”页上看到的选项是相同的   。

 **使用 Azure 帐户**  
 指定是否使用联机帐户。
  
 **存储帐户名称**  
 输入 Azure 存储帐户的名称。  
  
**帐户密钥**  
输入 Azure 存储帐户的密钥。  
  
 **使用 HTTPS**  
 指定是使用 HTTP 还是 HTTPS 连接到存储帐户。  
  
 **使用本地开发人员帐户**  
 指定是否在本地计算机上使用存储仿真程序。  
  
 **Blob 容器名称**  
 从指定的存储帐户中可用的存储容器列表中选择。  
  
 **Blob 文件格式**  
 选择文本或 Avro 文件格式。  
  
 **列分隔符字符**  
 如果选择文本格式，请输入列分隔符字符。  
  
 **使用第一行作为列名称**  
 指定第一行数据是否包含列名称。  

## <a name="see-also"></a>另请参阅
[选择数据源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[选择目标](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

