---
title: 修改 SQL 复制的快照初始化选项 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshot replication [SQL Server], options
- snapshots [SQL Server replication], options
ms.assetid: 759fab42-66c7-4541-a7a3-bb6fb868493c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2a611de458537156740521dae8b732eed3e2653c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63270256"
---
# <a name="modify-snapshot-initialization-options-for-sql-replication"></a>修改 SQL 复制的快照初始化选项

本文介绍如何修改大量选项[使用快照初始化订阅](initialize-a-subscription-with-a-snapshot.md)。

## <a name="snapshot-format"></a>快照格式
  在“发布属性 - \<发布>”对话框的“快照”页上指定快照格式。 有关访问此对话框的详细信息，请参阅 [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md)。  

1.  在“发布属性 - \<发布>”对话框的“快照”页上，选择“本机 SQL Server - 所有订阅服务器都必须是运行 SQL Server 的服务器”或“字符 - 如果发布服务器或订阅服务器没有运行 SQL Server，则需要此项”。 

    > [!NOTE]  
    >  建议选择本机格式，除非此发布必须支持对 [!INCLUDE[ssEW](../../../includes/ssew-md.md)] 数据库或非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库的订阅。    
1.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

## <a name="snapshot-folder-locations"></a>快照文件夹位置

### <a name="default-snapshot-location"></a>默认快照位置
指定默认快照位置上默认快照位置 (SQL Server Management Studio)**快照文件夹**配置分发向导的页。 有关使用此向导的详细信息，请参阅[配置发布和分发](configure-publishing-and-distribution.md)。 如果在未配置为分发服务器的服务器上创建发布，请在新建发布向导的 **“快照文件夹”** 页上指定默认快照位置。 有关使用此向导的详细信息，请参阅[创建发布](publish/create-a-publication.md)。  
  
 在“分发服务器属性 - \<分发服务器>”对话框的“发布服务器”页上，修改默认快照位置。 有关详细信息，请参阅[查看和修改分发服务器和发布服务器属性](view-and-modify-distributor-and-publisher-properties.md)。 在“发布属性 - \<发布>”对话框中设置每个发布的快照文件夹。 有关详细信息，请参阅 [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md)。  
  
#### <a name="modify-the-default-snapshot-location"></a>修改默认快照位置  
  
1.  在“分发服务器属性 - \<分发服务器>”对话框的“发布服务器”页上，单击要更改其默认快照位置的发布服务器的属性按钮 (…)。    
2.  在“分发服务器属性 - \<分发服务器>”对话框中，为“默认快照文件夹”属性输入一个值。

    > [!NOTE]  
    >  快照代理必须对指定的目录具有写权限，而分发代理或合并代理必须具有读权限。 如果使用的是请求订阅，则必须指定一个共享目录作为通用命名约定 (UNC) 路径，如 \\\computername\snapshot。 有关详细信息，请参阅[保护快照文件夹](security/secure-the-snapshot-folder.md)。    
1.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

### <a name="alternate-snapshot-location"></a>备用快照位置
  在“发布属性 - \<发布>”对话框的“快照”页上指定备用快照位置。 有关访问此对话框的详细信息，请参阅 [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md)。 

  
#### <a name="specify-an-alternate-snapshot-location"></a>指定备用快照位置  
  
1.  在“发布属性 - \<发布>”对话框的“快照”页上：    
    1.  选择 **“将文件放入下列文件夹”**，然后单击 **“浏览”** 定位到某个目录，或者输入用于存储快照文件的目录的路径。    

        > [!NOTE]  
        >  快照代理必须对指定的目录具有写权限，而分发代理或合并代理必须具有读权限。 如果使用的是请求订阅，则必须指定一个共享目录作为通用命名约定 (UNC) 路径，如 \\\computername\snapshot。 有关详细信息，请参阅[保护快照文件夹](security/secure-the-snapshot-folder.md)。    
    a.  除非需要将快照文件同时写入两个位置，否则应清除 **“将文件放入默认文件夹”** 。    
     若要压缩快照文件，请选择 **“压缩此文件夹中的快照文件”**。 压缩通常用于低带宽连接和可移动介质（如 CD-ROM）上的备用快照位置。    
1.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]   


## <a name="compress-snapshot-files"></a>压缩快照文件
指定应在“发布属性 - \<发布>”对话框的“快照”页上压缩文件。 有关访问此对话框的详细信息，请参阅 [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md)。  
  
1.  在“发布属性 - \<发布>”对话框的“快照”页上：  
  
    1.  选择 **“将文件放入下列文件夹”**，然后单击 **“浏览”** 定位到某个目录，或者输入用于存储快照文件的目录的路径。    
        > [!NOTE]  
        >  快照代理必须对指定的目录具有写权限，而分发代理或合并代理必须具有读权限。 如果使用的是请求订阅，则必须指定一个共享目录作为通用命名约定 (UNC) 路径，如 \\\computername\snapshot。 有关详细信息，请参阅[保护快照文件夹](security/secure-the-snapshot-folder.md)  
  
    2.  除非需要将快照文件同时写入两个位置，否则应清除 **“将文件放入默认文件夹”** 。    
        > [!NOTE]  
        >  如果选中了此复选框，则默认文件夹中存储的文件将不压缩。 压缩文件只能存储在上一步骤中指定的备用位置中。    
2.  选择 **“压缩此文件夹中的快照文件”**。    
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

## <a name="execute-scripts-before-and-after-snapshot-is-applied"></a>在应用快照之前和之后执行脚本

 可以指定在应用快照之前或之后在订阅服务器上执行的脚本。 使用脚本的原因有多种，例如在每台订阅服务器上创建登录帐户和架构（对象所有者）。  
  
 可以为每个脚本指定一个文件位置，每次发生快照处理时，快照代理都会将脚本文件复制到当前快照文件夹中。 应用快照时，分发代理或合并代理会在执行任何复制的对象脚本之前执行快照前脚本。 分发代理或合并代理在所有其他复制的对象脚本和数据应用之后，才会执行快照后脚本。 在完成快照应用程序且成功执行脚本文件之后，这些脚本文件将从订阅服务器上的工作目录中删除。  
  
 通过启动 **sqlcmd** 实用工具来执行脚本。 部署脚本之前，请先用 **sqlcmd** 执行该脚本，以确保它可以按预期方式执行。 应用快照之前和之后执行的脚本的内容必须可重复。 例如，如果在脚本中创建了一个表，则应该首先检查该表是否存在，如果存在就执行相应的操作。 脚本必须可重复是因为，如果需要重新初始化已应用了脚本的订阅，则在重新初始化期间应用新的快照时，将再次应用该脚本。  
  
 如果压缩快照文件（采用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] CAB 文件格式压缩），则也会压缩脚本并将其置于此 CAB 文件中。 压缩的快照文件传输到订阅服务器并解压缩到订阅服务器上的工作目录后，将执行所有指示为快照前脚本的脚本。 同样，在应用快照的最后一个步骤中，所有快照后脚本在订阅服务器上解压缩并执行。  

### <a name="execute-a-script-before-or-after-a-snapshot-is-applied"></a>应用快照前后执行脚本  
 在“发布属性 - \<发布>”对话框的“快照”页上，指定在应用快照前后执行的可选脚本。 有关访问此对话框的详细信息，请参阅 [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md)。  


1.  在“发布属性 - \<发布>”对话框的“快照”页上：    
    -   若要指定在应用快照之前执行的脚本，请单击 **“浏览”** 导航到该脚本，或者在 **“应用快照之前执行此脚本”** 文本框中输入该脚本的路径。 
   
        > [!NOTE]  
        >  分发代理或合并代理必须对指定目录具有读取权限。 如果使用的是请求订阅，则必须指定一个共享目录作为通用命名约定 (UNC) 路径，如 \\\computername\scripts\myscript.sql。    
    -   若要指定在应用快照之后执行的脚本，请单击 **“浏览”** 导航到该脚本，或者在 **“应用快照之后执行此脚本”** 文本框中输入该脚本的 UNC 路径。    
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
  
  
