---
title: 群集磁盘选择 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- cluster disk selection
ms.assetid: 0d6b863d-5972-4a20-9990-64ee8016fea6
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ea021ed6e3613d4a39641c582e0b091ebfe1a6f1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63063354"
---
# <a name="cluster-disk-selection"></a>群集磁盘选择
  使用 **安装向导的** “群集磁盘选择” [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 页为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集选择共享群集磁盘资源。 群集磁盘用于存放 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据。  
  
 共享的群集磁盘不是必要条件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)]群集安装。 SMB 文件服务器是为支持的存储[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)]故障转移群集安装，并可以通过使用指定**数据库引擎-数据目录**完成安装前的页。  
  
> [!WARNING]  
>  如果选择了要安装 Analysis Services，您必须指定共享群集磁盘。  
>   
>  如果您计划在此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集实例上启用 FILESTREAM，必须指定共享群集磁盘。  
  
## <a name="options"></a>选项  
 **共享的磁盘**  
 从列表中选择一个磁盘。 群集磁盘用于存放 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据。  
  
 只能指定一个磁盘。 如果选择包含群集仲裁资源的组，将显示警告。 建议不要安装到群集仲裁资源。  
  
 **可用共享的磁盘**  
 显示可用磁盘的列表，对于列表中的每个磁盘，均会显示是否可用作共享磁盘以及磁盘资源的说明。  
  
  
