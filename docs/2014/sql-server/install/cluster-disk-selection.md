---
title: 群集磁盘选择 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- cluster disk selection
ms.assetid: 0d6b863d-5972-4a20-9990-64ee8016fea6
caps.latest.revision: 9
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: ce08658fe769a356e4cd24e29ed094692892e48f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026063"
---
# <a name="cluster-disk-selection"></a>群集磁盘选择
  使用 **安装向导的** “群集磁盘选择” [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 页为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集选择共享群集磁盘资源。 群集磁盘用于存放 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据。  
  
 共享的群集磁盘不是必要条件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)]群集安装。 SMB 文件服务器是受支持的存储[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)]故障转移群集安装，并可以通过使用指定**数据库引擎 – 数据目录**页之前完成安装。  
  
> [!WARNING]  
>  如果选择了要安装 Analysis Services，您必须指定共享群集磁盘。  
>   
>  如果您计划在此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集实例上启用 FILESTREAM，必须指定共享群集磁盘。  
  
## <a name="options"></a>“常规”  
 **共享的磁盘**  
 从列表中选择一个磁盘。 群集磁盘用于存放 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据。  
  
 只能指定一个磁盘。 如果选择包含群集仲裁资源的组，将显示警告。 建议不要安装到群集仲裁资源。  
  
 **可用共享的磁盘**  
 显示可用磁盘的列表，对于列表中的每个磁盘，均会显示是否可用作共享磁盘以及磁盘资源的说明。  
  
  