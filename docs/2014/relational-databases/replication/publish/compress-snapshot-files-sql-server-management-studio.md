---
title: 压缩快照文件 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], compressed
- snapshot replication [SQL Server], compressed snapshots
ms.assetid: 174ade3e-74a1-4e67-a6da-b874be3ff50f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c8be85ae97d281113515205fadba9be827492474
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52762564"
---
# <a name="compress-snapshot-files-sql-server-management-studio"></a>压缩快照文件 (SQL Server Management Studio)
  指定应在“发布属性 - \<发布>”对话框的“快照”页上压缩文件。 有关访问此对话框的详细信息，请参阅 [View and Modify Publication Properties](view-and-modify-publication-properties.md)。  
  
### <a name="to-compress-snapshot-files"></a>压缩快照文件  
  
1.  在“发布属性 - \<发布>”对话框的“快照”页上：  
  
    1.  选择 **“将文件放入下列文件夹”**，然后单击 **“浏览”** 定位到某个目录，或者输入用于存储快照文件的目录的路径。  
  
        > [!NOTE]  
        >  快照代理必须对指定的目录具有写权限，而分发代理或合并代理必须具有读权限。 如果使用的是请求订阅，则必须指定一个共享目录作为通用命名约定 (UNC) 路径，如 \\\computername\snapshot。 有关详细信息，请参阅[保护快照文件夹](../security/secure-the-snapshot-folder.md)  
  
    2.  除非需要将快照文件同时写入两个位置，否则应清除 **“将文件放入默认文件夹”** 。  
  
        > [!NOTE]  
        >  如果选中了此复选框，则默认文件夹中存储的文件将不压缩。 压缩文件只能存储在上一步骤中指定的备用位置中。  
  
2.  选择 **“压缩此文件夹中的快照文件”**。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [配置快照属性（复制 Transact-SQL 编程）](configure-snapshot-properties-replication-transact-sql-programming.md)   
 [更改发布和项目属性](change-publication-and-article-properties.md)   
 [压缩的快照](../compressed-snapshots.md)   
 [使用快照初始化订阅](../initialize-a-subscription-with-a-snapshot.md)  
  
  
