---
title: 步骤 1： 配置 pyodbc Python 开发环境 |Microsoft Docs
ms.custom: ''
ms.date: 07/06/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 74e69704-e63c-450b-9207-5c1491d0e0f5
caps.latest.revision: 2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7f588174ea80677066628cb3e756d7c38bd42fba
ms.sourcegitcommit: 9cd01df88a8ceff9f514c112342950e03892b12c
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2018
ms.locfileid: "42785465"
---
# <a name="step-1-configure-development-environment-for-pyodbc-python-development"></a>步骤 1：配置用于 pyodbc Python 开发的开发环境

## <a name="windows"></a>Windows  
使用 Python-在 Windows 上的 pyodbc 连接到 SQL 数据库：
  
1. **下载 Python 安装程序**。  
  如果你的计算机不具有 Python，请将其安装。 转到[Python 下载页](https://www.python.org/downloads/windows/)并下载适当的安装程序。 例如，如果您是在 64 位计算机上，下载 Python 2.7 或 3.7 (x64) 安装程序。  
  
2. **安装 Python**。  下载安装程序后，执行以下步骤：。 双击该文件以启动安装程序。 B. 选择你的语言，并同意这些条款。 c. 按照屏幕上的说明，并应在计算机上安装 Python。 d. 你可以验证是否通过转到安装 Python`C:\Python27`或`C:\Python37`并运行`python -V`或`py -V`（适用于 3.x) 
      
3. [**在 Windows 上安装 Microsoft ODBC Driver for SQL Server**](../../odbc/windows/system-requirements-installation-and-driver-files.md#installing-microsoft-odbc-driver-for-sql-server)
  
4. **以管理员身份打开 cmd.exe**     

5. **使用 pip 的 Python 包管理器安装 pyodbc** (替换`C:\Python27\Scripts`与你已安装的 Python 路径)
```  
> cd C:\Python27\Scripts  
> pip install pyodbc  
```  

  
## <a name="linux"></a>Linux 
使用 Python-pyodbc 连接到 SQL 数据库：
  
1. **打开终端**  

2. [**在 Linux 上安装 Microsoft ODBC Driver for SQL Server**](../../odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)

3.  **安装 pyodbc**  
```  
> sudo -H pip install pyodbc
```
