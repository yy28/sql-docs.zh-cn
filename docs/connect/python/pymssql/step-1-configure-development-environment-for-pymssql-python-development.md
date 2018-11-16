---
title: 步骤 1： 配置 pymssql Python 开发环境 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6d392a5e-b08e-4b35-9e99-61260888fc41
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 623b4bf9a88031cf891e88f75c30b06716bb27ff
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2018
ms.locfileid: "51605017"
---
# <a name="step-1-configure-development-environment-for-pymssql-python-development"></a>步骤 1：配置用于 pymssql Python 开发的开发环境
你将需要在满足先决条件配置开发环境，以便开发使用 Python Driver for SQL Server 的应用程序。    
  
请注意，Python SQL 驱动程序使用 SQL Server 和 Azure SQL 数据库中的默认情况下启用的 TDS 协议。  这种方式无需任何其他配置。  
  
## <a name="windows"></a>Windows  
  
1. **安装 Python 运行时和 pip 包管理器**  
A. 转到[python.org](https://www.python.org/downloads/)  
B. 单击相应的 Windows 安装程序 msi 链接。   
c. 一次下载的运行 msi 安装 Python 运行时  
  
2. **下载 pymssql 模块**从[此处](https://www.lfd.uci.edu/~gohlke/pythonlibs/#pymssql)  
  
    请确保选择正确的 whl 文件。  例如： 如果正在 64 位计算机上使用 Python 2.7 选择： pymssql‑2.1.1‑cp27‑none‑win_amd64.whl。 一旦您下载.whl 文件会将它放在 c:/python27 文件夹中。  
      
3. **打开 cmd.exe**  
  
4. **安装 pymssql 模块**     
    例如，如果在 64 位计算机上使用 Python 2.7:  
```  
> cd c:\Python27  
> pip install pymssql‑2.1.1‑cp27‑none‑win_amd64.whl  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **安装 Python 运行时和 pip 包管理器**Python 可能已预安装大多数版本的 Ubuntu 上。  如果你的计算机没有安装 python，就可以下载从源 tarball [python.org](https://www.python.org/downloads/)和生成本地，也可以使用程序包管理器：  
```  
> sudo apt-get install python   
```  
  
2.  **打开终端**  
  
3.  **安装 pymssql 模块依赖项**  
```  
> sudo apt-get --assume-yes update  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
> sudo apt-get --assume-yes install python-dev python-pip  
> sudo pip install pymssql  
```  
  
## <a name="mac"></a>Mac  
  
1. **安装 Python 运行时和 pip 包管理器**  
A. 转到[python.org](https://www.python.org/downloads/)  
B. 单击相应的 Mac 安装程序 pkg 链接。   
c. 一次下载的运行 pkg 安装 Python 运行时  
  
2.  **打开终端**  
  
3. **安装 Homebrew 包管理器**  
```  
> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  
```  
  
4.  **安装 FreeTDS 模块**  
```  
> brew install FreeTDS  
```  
  
5.  **安装 pymssql 模块**  
```  
> sudo -H pip install pymssql  
```
