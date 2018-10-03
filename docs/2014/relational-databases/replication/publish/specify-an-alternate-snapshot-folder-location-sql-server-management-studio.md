---
title: 指定备用快照文件夹位置 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], alternate folder locations
- snapshot replication [SQL Server], alternate folder locations
- alternate snapshot folders [SQL Server replication]
ms.assetid: 9293f0eb-5531-47ec-b6e2-0392823ce5cc
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cae9676985ce2858d7eae1e2f6dc139ee6e4ed54
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48132947"
---
# <a name="specify-an-alternate-snapshot-folder-location-sql-server-management-studio"></a>指定备用快照文件夹位置 (SQL Server Management Studio)
  在“发布属性 - \<发布>”对话框的“快照”页上指定备用快照位置。 有关访问此对话框的详细信息，请参阅 [View and Modify Publication Properties](view-and-modify-publication-properties.md)。  
  
### <a name="to-specify-an-alternate-snapshot-location"></a>指定备用快照位置  
  
1.  在“发布属性 - \<发布>”对话框的“快照”页上：  
  
    1.  选择 **“将文件放入下列文件夹”**，然后单击 **“浏览”** 定位到某个目录，或者输入用于存储快照文件的目录的路径。  
  
        > [!NOTE]  
        >  快照代理必须对指定的目录具有写权限，而分发代理或合并代理必须具有读权限。 如果使用的是请求订阅，则必须指定一个共享目录作为通用命名约定 (UNC) 路径，如 \\\computername\snapshot。 有关详细信息，请参阅[保护快照文件夹](../security/secure-the-snapshot-folder.md)。  
  
    2.  除非需要将快照文件同时写入两个位置，否则应清除 **“将文件放入默认文件夹”** 。  
  
     若要压缩快照文件，请选择 **“压缩此文件夹中的快照文件”**。 压缩通常用于低带宽连接和可移动介质（如 CD-ROM）上的备用快照位置。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [备用快照文件夹位置](../alternate-snapshot-folder-locations.md)   
 [配置快照属性（复制 Transact-SQL 编程）](configure-snapshot-properties-replication-transact-sql-programming.md)   
 [指定默认快照位置 (SQL Server Management Studio)](../specify-the-default-snapshot-location-sql-server-management-studio.md)   
 [更改发布和项目属性](change-publication-and-article-properties.md)   
 [使用快照初始化订阅](../initialize-a-subscription-with-a-snapshot.md)  
  
  
