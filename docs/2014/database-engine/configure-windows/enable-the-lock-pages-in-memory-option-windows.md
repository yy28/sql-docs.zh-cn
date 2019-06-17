---
title: 启用“锁定内存页”选项 (Windows) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Lock Pages in Memory option
ms.assetid: cd581fbc-4747-439e-87f9-2f18e39c5bb9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0f6e938e3212e519ab51be1faf3f18e28957ef3e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62782275"
---
# <a name="enable-the-lock-pages-in-memory-option-windows"></a>启用“锁定内存页”选项 (Windows)
  此 Windows 策略将确定哪些帐户可以使用进程将数据保留在物理内存中，从而阻止系统将数据分页到磁盘的虚拟内存中。  
  
> [!NOTE]  
>  当预计会将内存分页到磁盘时，锁定内存中的页可以大大提高性能。  
  
 使用 Windows 组策略工具 (gpedit.msc)，可以为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用的帐户启用此策略。 必须是系统管理员才能更改此策略。  
  
### <a name="to-enable-the-lock-pages-in-memory-option"></a>启用“锁定内存页”选项  
  
1.  在 **“开始”** 菜单上，单击 **“运行”** 。 在中**开放**框中，键入`gpedit.msc`。  
  
2.  在 **“本地组策略编辑器”** 控制台上，展开 **“计算机配置”** ，再展开 **“Windows 设置”** 。  
  
3.  展开 **“安全设置”** ，再展开 **“本地策略”** 。  
  
4.  选择 **“用户权利指派”** 文件夹。  
  
     细节窗格中随即显示出策略。  
  
5.  在该窗格中，双击“锁定内存页”  。  
  
6.  在“本地安全设置 - 锁定内存中的页”对话框中，单击“添加用户或组”   。  
  
7.  在 **“选择用户、服务帐户或组”** 对话框中，添加有权运行 sqlservr.exe 的帐户。  
  
8.  注销后重新登录，此更改才生效。  
  
## <a name="see-also"></a>请参阅  
 [“服务器内存”服务器配置选项](server-memory-server-configuration-options.md)  
  
  
