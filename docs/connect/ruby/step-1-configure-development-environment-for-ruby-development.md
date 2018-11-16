---
title: 步骤 1：配置用于 Ruby 开发的开发环境 | Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8cdbadeb-f640-406c-977c-d2d44b7b5368
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a298a7c7f65a198e5bfb0922f2b061fd44079739
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2018
ms.locfileid: "51604697"
---
# <a name="step-1-configure-development-environment-for-ruby-development"></a>步骤 1：配置用于 Ruby 开发的开发环境
你将需要在满足先决条件配置开发环境，以便开发使用 Ruby Driver for SQL Server 的应用程序。    
  
请注意，Ruby 驱动程序使用 SQL Server 和 Azure SQL 数据库中的默认情况下启用的 TDS 协议。  这种方式无需任何其他配置。  
  
  
## <a name="windows"></a>Windows  
  
1.  **下载 Ruby 安装程序**  
如果你的计算机没有 Ruby，请安装它。 对于新的 ruby 用户，我们建议使用 Ruby 2.2.X 安装程序。 它们提供的稳定语言和扩展的包 (gem) 兼容的和已更新的列表。 转[Ruby 下载页](https://rubyinstaller.org/downloads/)并下载合适的 2.1.x 安装程序。 有关示例，如果您是在 64 位计算机上，下载 Ruby 2.1.6 (x64) 安装程序。   
  
2.  **安装 Ruby**  
下载安装程序后，请执行以下操作：  
A. 双击该文件以启动安装程序。  
B. 选择你的语言，并同意这些条款。  
c.  在安装设置屏幕中，选择对路径并关联.rb 和.rbw 文件与此 Ruby 安装这两个添加 Ruby 可执行文件旁边的复选框。  
  
3.  **下载 Ruby DevKit**  
从 RubyInstaller 页下载 DevKit  
  
4.  **安装 Ruby DevKit**  
下载完成后，请执行以下操作：  
A. 双击该文件。 将要求中提取文件的位置。  
B. 单击"..."按钮，然后选择"C:\DevKit"。 可能需要通过单击"新建文件夹"首次创建此文件夹。  
c. 单击"确定"，并单击"解压缩"，以提取文件。  
  
5. **打开 cmd.exe**  
  
6. **初始化 Ruby DevKit**  
```  
> chdir C:\DevKit  
> ruby dk.rb init  
> ruby dk.rb install  
```  
  
7.  **安装 TinyTDS gem**  
```  
> gem inst tiny_tds
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **打开终端**  
  
2. **安装 Ruby 版本管理器 (rvm) 和必备组件**  
```  
> sudo apt-get --assume-yes update  
> command curl -sSL https://rvm.io/mpapis.asc | gpg --import -  
> curl -L https://get.rvm.io | bash -s stable  
> source ~/.rvm/scripts/rvm  
```  
   
3. **使用 rvm 安装 Ruby**  
例如，安装 Ruby 的版本 2.3.0:  
```  
> rvm install 2.3.0  
> rvm use 2.3.0 --default  
> ruby -v  
```  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;请确保最后一个命令的输出将指示运行版本 2.3.0。  
  
4.  **安装 FreeTDS**  
```  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
```  
  
5.  **安装 TinyTDS**  
```  
> gem install tiny_tds  
```  
  
## <a name="mac"></a>Mac  
  
请注意，Mac OS X 已有 Ruby 预安装，因为操作系统有依赖关系。    
  
1.  **打开终端**  
  
2. **安装 Homebrew 包管理器**  
```  
> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  
```  
  
3.  **安装 FreeTDS**  
```  
> brew install FreeTDS  
```  
  
4.  **安装 TinyTDS gem**  
```  
> gem install tiny_tds  
```
