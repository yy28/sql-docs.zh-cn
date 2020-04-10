---
title: 步骤 1：配置 pyodbc Python 开发环境 | Microsoft Docs
ms.custom: ''
ms.date: 07/06/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 74e69704-e63c-450b-9207-5c1491d0e0f5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7dd2063a527d782833f2abfcbd635de30aa27117
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80926779"
---
# <a name="step-1-configure-development-environment-for-pyodbc-python-development"></a>步骤 1：配置用于 pyodbc Python 开发的开发环境

## <a name="windows"></a>Windows  
在 Windows上使用 Python - pyodbc 连接到 SQL 数据库：
  
1. **下载 Python 安装程序**。  
  如果计算机上没有 Python，请安装它。 转到 [Python 下载页](https://www.python.org/downloads/windows/)，并下载相应的安装程序。 例如，如果使用的是 64 位计算机，请下载 Python 2.7 或 3.7 (x64) 安装程序。  
  
2. **安装 Python**。  下载安装程序后，请按照以下步骤操作：a. 双击文件，以启动安装程序。 b. 选择语言，并同意接受条款。 c. 按照屏幕上的说明操作，然后 Python 就应该安装在计算机上了。 d. 可以通过转到 `C:\Python27` 或 `C:\Python37` 并运行 `python -V` 或 `py -V`（对于 3.x）来验证 Python 是否已安装 
      
3. [**在 Windows 上安装 Microsoft ODBC Driver for SQL Server**](../../odbc/windows/system-requirements-installation-and-driver-files.md#installing-microsoft-odbc-driver-for-sql-server)
  
4. **以管理员身份打开 cmd.exe**     

5. **使用 pip - Python 包管理器安装 pyodbc**（将 `C:\Python27\Scripts` 替换为 Python 安装路径）
```  
> cd C:\Python27\Scripts  
> pip install pyodbc  
```  

  
## <a name="linux"></a>Linux 
使用 Python - pyodbc 连接到 SQL 数据库：
  
1. **打开终端**  

2. [**在 Linux 上安装 Microsoft ODBC Driver for SQL Server**](../../odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)

3.  **安装 pyodbc**  
```  
> sudo -H pip install pyodbc
```
