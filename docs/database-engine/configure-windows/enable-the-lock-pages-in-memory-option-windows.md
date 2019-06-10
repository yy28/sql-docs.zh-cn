---
title: 启用“锁定内存页”选项 (Windows) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Lock Pages in Memory option
ms.assetid: cd581fbc-4747-439e-87f9-2f18e39c5bb9
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: ed3ab4323780401226d58c1eaffd47616f1f42f2
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66783665"
---
# <a name="enable-the-lock-pages-in-memory-option-windows"></a>启用“锁定内存页”选项 (Windows)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  此 Windows 策略将确定哪些帐户可以使用进程将数据保留在物理内存中，从而阻止系统将数据分页到磁盘的虚拟内存中。  
  
> [!NOTE]  
>  当预计会将内存分页到磁盘时，锁定内存中的页可以大大提高性能。  
  
 使用 Windows 组策略工具 (gpedit.msc)，可以为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用的帐户启用此策略。 必须是系统管理员才能更改此策略。  
  
### <a name="to-enable-the-lock-pages-in-memory-option"></a>启用“锁定内存页”选项  
  
1.  在 **“开始”** 菜单上，单击 **“运行”** 。 在“打开”  框中，键入 **gpedit.msc**  
  
2.  在 **“本地组策略编辑器”** 控制台上，展开 **“计算机配置”** ，再展开 **“Windows 设置”** 。  
  
3.  展开 **“安全设置”** ，再展开 **“本地策略”** 。  
  
4.  选择 **“用户权利指派”** 文件夹。  
  
     细节窗格中随即显示出策略。  
  
5.  在该窗格中，双击“锁定内存页”  。  
  
6.  在“本地安全设置 - 锁定内存中的页”对话框中，单击“添加用户或组”   。  
  
7.  在“选择用户”、“服务帐户”或“组”对话框中，选择 SQL Server 服务帐户  。  
  
8.  重启 SQL Server 服务，以使此设置生效。
  
## <a name="see-also"></a>另请参阅  
 [“服务器内存”服务器配置选项](../../database-engine/configure-windows/server-memory-server-configuration-options.md)  
  
  
