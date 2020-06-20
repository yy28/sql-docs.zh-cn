---
title: 从命令提示符安装升级顾问 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- installing Upgrade Advisor
- command prompt [Upgrade Advisor]
- Setup [Upgrade Advisor]
- Upgrade Advisor [SQL Server], installing
ms.assetid: a6841cc2-ca13-4b1c-9343-9e4d54312c3a
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 738e1ef203f4c9c83e42c7d8255f82978465eadf
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065289"
---
# <a name="installing-upgrade-advisor-from-the-command-prompt"></a>从命令提示符安装升级顾问
  您可以使用安装向导或从命令提示符安装升级顾问。 使用命令提示符，可以执行无人参与的自动安装。  
  
## <a name="installation-syntax"></a>安装语法  
 从命令提示符安装升级顾问的基本语法如下：  
  
 `SQLUA.msi [options]`  
  
 下表列出了最常用的选项。  
  
|参数|说明|  
|--------------|-----------------|  
|/q [n&#124;b&#124;r&#124;f]|设置用户界面 (UI) 级别：<br /><br /> n = 无 UI<br /><br /> b = 基本 UI（仅显示进度，不显示提示）<br /><br /> r = 简化的 UI（在安装结束时显示对话框）<br /><br /> f = 完整的 UI|  
|/L|指定日志文件选项。 若要将所有消息记录到*log_file_name*，请使用 **-L \* v**_log_file_name_。 若要仅记录错误消息，请使用 `-Le` *log_file_name*。|  
|ADDLOCAL = ALL&#124; REMOVE = ALL&#124;重新安装 = 全部|指定安装 (ADDLOCAL)、删除 (REMOVE) 或重新安装 (REINSTALL) 升级顾问。|  
|UAINSTALLDIR=路径|将升级顾问安装到路径指定的位置。|  
  
## <a name="installation-examples"></a>安装示例  
 下面的示例说明如何使用命令提示符安装升级顾问：  
  
```  
SQLUA.msi /qn ADDLOCAL=ALL UAINSTALLDIR="C:\Upgrade Advisor"  
```  
  
 您也可以在运行此命令时使用 Msiexec 程序：  
  
```  
Msiexec.exe /i C:\Downloads\SQLUA.msi /qn ADDLOCAL=ALL UAINSTALLDIR="C:\Upgrade Advisor"  
```  
  
 如果必须使用其他安装选项，这一方法会很有帮助。  
  
## <a name="removal-examples"></a>删除示例  
 下面的示例说明如何使用命令提示符删除升级顾问：  
  
```  
SQLUA.msi /qn REMOVE=ALL  
```  
  
 您也可以在运行此命令时使用 Msiexec 程序：  
  
```  
Msiexec.exe /i C:\Downloads\SQLUA.msi /qn REMOVE=ALL  
```  
  
## <a name="see-also"></a>另请参阅  
 [安装升级顾问](../../../2014/sql-server/install/installing-upgrade-advisor.md)   
 [升级顾问必备组件](../../../2014/sql-server/install/upgrade-advisor-prerequisites.md)  
  
  
