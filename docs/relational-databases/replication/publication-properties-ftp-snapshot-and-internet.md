---
title: "发布属性，FTP 快照和 Internet | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newpubwizard.pubproperties.internetsynchronization.f1"
ms.assetid: 8e0198c3-5e4e-418c-9920-78ccbbfc1323
caps.latest.revision: 25
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 25
---
# 发布属性，FTP 快照和 Internet
  使用此页，您可以：  
  
-   设置通过文件传输协议 (FTP) 传递快照的属性。 有关详细信息，请参阅 [通过 FTP 传输快照](../../relational-databases/replication/transfer-snapshots-through-ftp.md)。 若要使用 FTP 传递快照，则必须设置 FTP 服务器。 有关详细信息，请参阅 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 文档。  
  
    > [!NOTE]  
    >  对任意 FTP 设置的更改都要求生成新的快照。  
  
-   设置 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更高版本上合并复制的 Web 同步的属性，Web 同步允许通过 HTTPS（安全超文本传输协议）来同步订阅。 若要使用 Web 同步，则必须配置 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet 信息服务 (IIS) 服务器。 有关详细信息，请参阅 [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md)。  
  
## 选项  
 **通过 FTP 访问快照文件**  
 选择 **允许订阅服务器下载快照文件使用 FTP （文件传输协议）**, ，并指定 **FTP 服务器名称**, ，**端口号**, ，**从 FTP 根文件夹的路径**, ，**Login**, ，和 **密码**, ，以允许使用 FTP 传递快照的订阅服务器。  
  
 此选项允许订阅服务器使用 FTP 检索快照文件，但不要求订阅服务器进行此操作。 如果选择此选项，新建订阅向导将默认为允许订阅服务器通过 FTP 检索快照文件。 若要更改该设置，请使用 **“订阅属性”** 对话框。 如果允许订阅服务器通过 FTP 访问快照文件，请将 FTP 文件夹指定为 **“发布属性”** 对话框的 **“快照”** 页上快照文件的位置。 这会导致在生成新快照时快照代理将自动更新 FTP 文件夹中的文件。 如果未将快照文件的位置设置为 FTP 文件夹，则在生成新快照时必须手动更新文件。 有关详细信息，请参阅 [提供快照通过 FTP](../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md)。  
  
 **Web 同步**  
 仅限合并复制。 若要允许合并订阅服务器使用 Web 同步，请选择 **“允许订阅服务器通过连接到 Web 服务器进行同步”**，并指定 Web 服务器地址。 Web 服务器必须使用安全套接字层 (SSL)，并且 Web 地址必须为完全限定地址，如 https://server.domain.com/synchronize。 有关详细信息，请参阅 [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md)。  
  
## 另请参阅  
 [创建发布](../../relational-databases/replication/publish/create-a-publication.md)   
 [查看和修改发布属性](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [查看和修改请求订阅属性](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [查看和修改推送订阅属性](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [创建并应用初始快照](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [发布数据和数据库对象](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  