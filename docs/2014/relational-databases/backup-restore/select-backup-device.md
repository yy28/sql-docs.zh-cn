---
title: 选择备份设备 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.selectbackupdevice.f1
ms.assetid: 7887c9fd-15ce-4cc8-b069-845c1d09088c
caps.latest.revision: 26
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 6135239b182c66ae4622dcf9af704fb30f167f6f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36025484"
---
# <a name="select-backup-device"></a>选择备份设备
  使用 **“选择备份设备”** 对话框可以选择还原操作使用的逻辑备份设备。  
  
 逻辑备份设备是与物理设备对应的用户定义的逻辑设备，它是操作系统提供的磁带机或磁盘驱动器。  
  
> [!NOTE]  
>  如果备份使用多个备份设备，这些设备必须与单一类型的设备相对应。  
  
 **使用 SQL Server Management Studio 查看备份设备的内容**  
  
-   [查看备份磁带或文件的内容 (SQL Server)](view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [查看逻辑备份设备的属性和内容 (SQL Server)](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
## <a name="options"></a>“常规”  
 **备份设备**  
 在该列表框中，选择要从中进行还原的逻辑备份设备的名称。  
  
 有关如何查看备份设备内容的信息，请参阅 [查看逻辑备份设备的属性和内容 (SQL Server)](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)。  
  
## <a name="remarks"></a>Remarks  
 如果您在列表中看不到包含所查找备份的逻辑备份设备，则备份可能已直接写入一个或多个文件或磁带机中。 在此情况下，请取消 **“选择备份设备”** 对话框；并在 **“指定备份”** 对话框中的 **“备份介质”** 列表框中选择 **“文件”** 或 **“磁带”** 。  
  
## <a name="see-also"></a>请参阅  
 [备份设备 (SQL Server)](backup-devices-sql-server.md)  
  
  