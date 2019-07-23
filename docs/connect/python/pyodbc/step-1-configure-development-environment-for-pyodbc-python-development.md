---
title: '步骤 1: 配置 pyodbc Python 开发环境 |Microsoft Docs'
ms.custom: ''
ms.date: 07/06/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 74e69704-e63c-450b-9207-5c1491d0e0f5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a1a43540d866faaf79b1c020eb255689862e6d97
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992518"
---
# <a name="step-1-configure-development-environment-for-pyodbc-python-development"></a>步骤 1：配置用于 pyodbc Python 开发的开发环境

## <a name="windows"></a>Windows  
在 Windows 上使用 Python-pyodbc 连接到 SQL 数据库:
  
1. **下载 Python 安装程序**。  
  如果计算机没有 Python, 请安装它。 请参阅[Python 下载页](https://www.python.org/downloads/windows/), 下载相应的安装程序。 例如, 如果你使用的是64位计算机, 请下载 Python 2.7 或 3.7 (x64) 安装程序。  
  
2. **安装 Python**。  下载安装程序后, 请执行以下步骤: a。 双击该文件以启动安装程序。 B. 选择语言, 并同意条款。 c. 按照屏幕上的说明进行操作, 并在计算机上安装 Python。 d. 可以通过转`C:\Python27`到或`C:\Python37`并运行`python -V`或`py -V` (适用于 2.x) 来验证是否已安装 Python 
      
3. [**在 Windows 上安装 Microsoft ODBC Driver for SQL Server**](../../odbc/windows/system-requirements-installation-and-driver-files.md#installing-microsoft-odbc-driver-for-sql-server)
  
4. **以管理员身份打开 cmd.exe**     

5. **使用 pip-Python 包管理器安装 pyodbc**(替换`C:\Python27\Scripts`为已安装的 Python 路径)
```  
> cd C:\Python27\Scripts  
> pip install pyodbc  
```  

  
## <a name="linux"></a>Linux 
使用 Python 连接到 SQL 数据库-pyodbc:
  
1. **打开终端**  

2. [**在 Linux 上安装 Microsoft ODBC Driver for SQL Server**](../../odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)

3.  **安装 pyodbc**  
```  
> sudo -H pip install pyodbc
```
