---
title: 配置磁盘空间使用情况 (PowerPivot for SharePoint) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 201a3fda-f162-45d7-bf39-74dcb92fd0e6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fc45827a349dc38054db98e3a435f18a42bdaa0f
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66071812"
---
# <a name="configure-disk-space-usage-powerpivot-for-sharepoint"></a>配置磁盘空间使用情况 (PowerPivot for SharePoint)
  PowerPivot for SharePoint 部署使用主机上的磁盘空间来缓存 PowerPivot 数据库以便更快地重新加载。 在内存中加载的每个 PowerPivot 数据库首先缓存到磁盘，以便以后可以更快地重新加载来支持新请求。 默认情况下，PowerPivot for SharePoint 使用所有可用磁盘空间来缓存其数据库，但是可以通过设置限制磁盘空间使用量的属性来修改此行为。  
  
 本主题介绍了如何设置磁盘空间使用限制。  
  
 本主题并不指导如何对在内容数据库中存储的 PowerPivot 数据库（嵌入在 Excel 工作簿中）进行磁盘空间管理。 PowerPivot 数据库可能会很大，因此对场的存储容量提出新要求。 此外，如果启用版本控制，您可能会很容易地在同一内容数据库中具有数据的多个副本，这进一步增加了内容存储所需的磁盘空间量。 尽管 PowerPivot 数据库是进行磁盘管理的重要考虑因素，但不能独立于在 SharePoint 场中存储的其他内容单独对该数据库进行管理。 在您的业务更频繁地使用 PowerPivot 工作簿时，您需要更紧密地对磁盘空间进行监视。 您还可以在 PowerPivot 管理面板中跟踪 PowerPivot 工作簿活动并且删除不再使用的工作簿。  
  
## <a name="how-powerpivot-for-sharepoint-manages-cached-databases"></a>PowerPivot for SharePoint 如何管理缓存的数据库  
 为了管理缓存，PowerPivot 系统服务将定期运行后台作业，以便清除内容库中具有更新版本的未使用或过期的数据库。 清除作业的目的是从内存卸载处于非活动状态的数据库，并从文件系统中删除未使用的缓存数据库。 该清除作业用于长期维护，确保数据库不会无限期保留在系统中。 在活动服务器上，数据库可能会由于服务器上的内存压力、SharePoint 中的数据库删除或内容库中数据库的更新的版本而更频繁地被删除。  
  
 尽管您不能计划该清除作业，但可以通过设置执行以下任务的服务器配置属性自定义缓存文件管理：  
  
-   设置缓存使用的磁盘空间量限制。  
  
-   指定在达到最大磁盘空间时要删除多少数据。  
  
## <a name="how-to-check-disk-space-usage"></a>如何检查磁盘空间使用情况  
 PowerPivot for SharePoint 安装在 SharePoint 场的应用程序服务器中。 每个安装都具有包含备份文件夹的数据字典。 备份文件夹包含 Analysis Services 实例在计算机上缓存的所有数据文件。 默认情况下，可在以下路径中找到该备份文件夹：  
  
 `%drive%:\Program Files\Microsoft SQL Server\MSAS10_50.PowerPivot\OLAP\Backup\Sandboxes\<serviceApplicationName>`  
  
 若要检查缓存一共占用了多少磁盘空间，您必须检查备份文件夹的大小。 在管理中心没有报告当前缓存大小的属性。  
  
 备份文件夹为在本地计算机的内存中加载的所有 PowerPivot 数据库提供公共的缓存存储区。 如果您在场中定义了多个 PowerPivot 服务应用程序，则这些应用程序都可以使用本地服务器来加载并随后缓存 PowerPivot 数据。 数据加载和缓存都是 Analysis Services 服务器操作。 同样，将在 Analysis Services 实例级别在备份文件夹上管理总磁盘空间使用量。 因此在 SharePoint 应用程序服务器上运行的单个 SQL Server Analysis Services 实例上设置限制磁盘空间使用的配置设置。  
  
 缓存仅包含 PowerPivot 数据库。 PowerPivot 数据库存储在单个父文件夹（备份文件夹）下的多个文件中。 因为 PowerPivot 数据库旨在用作 Excel 工作簿的内部数据，所以，数据库名称是基于 GUID 的，而非说明性名称。 下的 GUID 文件夹 **\<serviceApplicationName >** 是 PowerPivot 数据库的父文件夹。 在多个 PowerPivot 数据库加载到服务器上时，为每个数据库都创建附加的文件夹。  
  
 因为 PowerPivot 数据可以加载到场中的任何 Analysis Services 实例上，所以，也可以在场中的多个计算机上缓存相同的数据。 与磁盘空间使用情况相比，此行为更为看重性能，但如果数据已经可用于磁盘，用户可以更快地访问数据。  
  
 若要立即减少磁盘空间使用，您可以关闭服务，然后从备份文件夹中删除 PowerPivot 数据库。 手动删除文件仅是暂时措施，因为在下次查询 PowerPivot 数据时，将再次缓存该数据库的更新的副本。 永久的解决办法包括限制缓存使用的磁盘空间。  
  
 在系统级别，您可以创建电子邮件警报，在磁盘空间不足时通知您。 Microsoft 系统中心包括电子邮件警报功能。 您还可以使用文件服务器资源管理器、任务计划程序或 PowerShell 脚本来设置警报。 以下链接提供一些有用的信息，可帮助您设置在磁盘空间不足时发出的通知：  
  
-   [什么是文件服务器资源管理器的新增](https://technet.microsoft.com/library/hh831746.aspx)(https://technet.microsoft.com/library/hh831746.aspx)。  
  
-   [适用于 Windows Server 2008 R2 文件服务器资源管理器分步指南](https://go.microsoft.com/fwlink/?LinkID=204875)(https://go.microsoft.com/fwlink/?LinkID=204875)。  
  
-   [Windows Server 2008 上设置磁盘空间不足警报](https://go.microsoft.com/fwlink/?LinkID=204870)( https://go.microsoft.com/fwlink/?LinkID=204870)。  
  
## <a name="how-to-limit-the-amount-of-disk-space-used-for-storing-cached-files"></a>如何限制用于存储缓存文件的磁盘空间量  
  
1.  在“管理中心”的“应用程序管理”中，单击 **“管理服务器上的服务”**。  
  
2.  单击 **SQL Server Analysis Services**。  
  
     请注意对在物理服务器上运行的 Analysis Services 实例设置限制，而非在服务应用程序级别设置限制。 使用本地 Analysis Services 实例的所有服务应用程序都受到为该实例设置的单个最大磁盘空间的限制。  
  
3.  在“磁盘使用情况”中，设置“总磁盘空间”的值 (GB) 以便设置用于缓存的空间量的上限。 默认值为 0，它允许 Analysis Services 使用所有可用磁盘空间。  
  
4.  磁盘使用情况，在**删除缓存的数据库中最后 'n' 小时**设置，指定磁盘空间达到最大限制时清空缓存的上次使用的条件。  
  
     默认值为 4 小时，这表示 4 小时或更长时间未处于活动状态的所有数据库都将从文件系统中删除。 处于非活动状态但仍在内存中的数据库将被卸载，然后从文件系统中删除。  
  
## <a name="how-to-limit-how-long-a-database-is-kept-in-the-cache"></a>如何限制数据库保留在缓存中的时间长度  
  
1.  在“管理中心”的“应用程序管理”中，单击 **“管理服务应用程序”**。  
  
2.  单击**默认 PowerPivot 服务应用程序**以打开管理仪表板。  
  
3.  在“操作”中，单击 **“配置服务应用程序设置”**。  
  
4.  在“磁盘缓存”部分中，您可以指定非活动数据库保留在内存中以便支持新请求的时间长度（默认为 48 小时）以及该数据库保留在缓存中的时间长度（默认为 120 小时）。  
  
     **“在内存中保留非活动数据库”** 指定非活动数据库保留在内存中以便支持针对这些数据的新请求的时间长度。 只要您对活动数据库进行查询，该活动数据库就会始终保留在内存中，但在该数据库不再处于活动状态后，系统会将该数据库在内存中再保留一段时间，以防出现针对这些数据的更多请求。  
  
     因为 PowerPivot 数据库首先缓存，然后在内存中加载，所以，数据库文件将立即占用磁盘空间。 但在数据库处于活动状态（以及此后的 48 小时）时，所有请求将首先定向到内存中数据库，并且忽略缓存的数据库。 在 48 小时的非活动期后，该文件将从内存中卸载，但仍保留在缓存中，在其中，如果本地 PowerPivot 服务器实例截获了针对该数据的新的连接请求，可以很快地重新加载这些数据。 从缓存而非内容库支持对非活动数据库的连接请求，并且尽量减小对内容数据库的影响。  
  
     特别要注意的是，内容库仅对于 PowerPivot 数据库而言是永久位置。 只有在库中的数据库与磁盘上的副本相同时，才使用缓存的副本。  
  
     **“在缓存中保留非活动数据库”** 指定非活动数据库在文件系统上保留多长时间后，将会从内存中卸载。 清除作业将使用此设置来确定要删除的文件。 168 小时（48 小时在内存中，120 小时在缓存中）处于非活动状态的所有 PowerPivot 数据库都将由清除作业从磁盘中删除。  
  
5.  单击 **“确定”** 保存所做的更改。  
  
## <a name="next-steps"></a>后续步骤  
 PowerPivot for SharePoint 安装提供运行状况规则，以便您可以在服务器运行状况、配置或可用性中检测到问题时采取纠正措施。 其中某些规则使用配置设置来确定触发运行状况规则的条件。 如果您在主动优化服务器性能，则最好还要检查这些设置以便确保默认值最适合您的系统。 有关详细信息，请参阅[PowerPivot 运行状况规则-配置](configure-power-pivot-health-rules.md)。  
  
## <a name="see-also"></a>请参阅  
 [在管理中心中管理和配置 PowerPivot 服务器](power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
  
