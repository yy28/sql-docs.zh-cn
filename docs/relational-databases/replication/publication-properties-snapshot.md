---
title: 发布属性 - 快照 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.pubproperties.snapshotformat.f1
ms.assetid: 8e9133b1-fc37-4a85-8a7c-d5eaf172fbef
caps.latest.revision: 24
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: dfef79d0fb54e078d9d263cc619a6993d53e4ca4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32961772"
---
# <a name="publication-properties-snapshot"></a>发布属性，快照
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  可以使用 **“发布属性”** 对话框的 **“快照”** 页设置快照格式、快照文件夹位置以及应用快照前后运行的脚本。 快照文件夹必须指定为共享文件夹，并且对于将文件读/写到快照文件夹的代理有足够的权限。 有关正确保护文件夹的详细信息，请参阅[保护快照文件夹的安全](../../relational-databases/replication/security/secure-the-snapshot-folder.md)。  
  
> [!NOTE]  
>  若要进行更改，则需要发布的新快照。 有关详细信息，请参阅[更改发布和项目属性](../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
## <a name="options"></a>“常规”  
 **快照格式**  
 选择快照格式的本机模式或字符模式。  
  
-   如果所有订阅服务器都是  的实例，而不是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例，请选择 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEW](../../includes/ssew-md.md)]. 本机快照格式可以提供最佳性能。  
  
-   如果有任何订阅服务器正在运行 **，或者为非** 订阅服务器，请选择 [!INCLUDE[ssEW](../../includes/ssew-md.md)] “字符 - 如果发布服务器或订阅服务器没有运行 SQL Server，则需要此项”[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 **快照文件的位置**  
 选择要存储快照文件的位置。 可以将快照文件存储在默认位置，也可以将其存储在默认位置之外的其他位置。 可以压缩存储在其他位置的文件。  
  
-   选择 **“将文件放入默认文件夹”** 可以使用发布服务器的默认快照文件夹。 此对话框中的快照文件夹位置是只读的，因为对于发布服务器来说，只能在 **“分发服务器属性”** 对话框中更改该位置。 有关详细信息，请参阅[指定默认快照位置 (SQL Server Management Studio)](../../relational-databases/replication/specify-the-default-snapshot-location-sql-server-management-studio.md)。  
  
-   选择 **“将文件放入下列文件夹”** 可以指定默认位置之外的其他位置。 在文本框中输入路径，或单击 **“浏览”** 定位到某个位置。 选择 **“压缩此文件夹中的快照文件”** 可以压缩其他快照位置中的文件。 其他位置可以为其他服务器、网络驱动器或诸如 CD-ROM、可移动磁盘等可移动介质上。 有关详细信息，请参阅 [Alternate Snapshot Folder Locations](../../relational-databases/replication/alternate-snapshot-folder-locations.md) 和 [Compressed Snapshots](../../relational-databases/replication/compressed-snapshots.md)。  
  
 **运行其他脚本**  
 指定在订阅服务器上应用快照之前和之后要执行的脚本。 如果 **“快照格式”** 为 **“字符”**，则不能指定脚本。  
  
 脚本是可选的，不过，脚本提供了一种便捷方法，可以在订阅服务器上执行命令和应用管理更改。 有关执行脚本的详细信息，请参阅[在应用快照之前和之后执行脚本](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md)。  
  
-   在 **“应用快照之前执行此脚本”** 文本框中输入路径，或单击 **“浏览”** 指定脚本的位置。  
  
-   在 **“应用快照之后执行此脚本”** 文本框中输入路径，或单击 **“浏览”** 指定脚本的位置。  
  
## <a name="see-also"></a>另请参阅  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [查看和修改发布属性](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [创建并应用初始快照](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [使用快照初始化订阅](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [发布数据和数据库对象](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
