# [关于 Linux 上的 SQL Server](sql-server-linux-overview.md)

# 概述
## [发行说明](sql-server-linux-release-notes.md)
## [此版本中有什么新增功能？](sql-server-linux-whats-new.md)
## [新的和已更新的项目](new-updated-linux.md)
## [版本和支持的功能](sql-server-linux-editions-and-components-2017.md)

# 快速入门
## [安装和连接 - Red Hat](quickstart-install-connect-red-hat.md)
## [安装和连接 - SUSE](quickstart-install-connect-suse.md)
## [安装和连接 - Ubuntu](quickstart-install-connect-ubuntu.md)
## [运行和连接 - Docker](quickstart-install-connect-docker.md)
## [在 Azure 中预配 SQL VM](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)
## [运行和连接 - 云](quickstart-install-connect-clouds.md)

# 教程
## [1_从 Windows 迁移](sql-server-linux-migrate-restore-database.md)
## [2_从 Oracle 迁移](../ssma/oracle/sql-server-linux-convert-from-oracle.md?toc=%2fsql%2flinux%2ftoc.json)
## [3_迁移到 Docker](tutorial-restore-backup-in-sql-server-container.md)
## [4_创建作业](sql-server-linux-run-sql-server-agent-job.md)
## [5_设置 AD 身份验证](sql-server-linux-active-directory-authentication.md)
## [6_创建故障转移群集实例](sql-server-linux-shared-disk-cluster-configure.md)
### [iSCSI](sql-server-linux-shared-disk-cluster-configure-iscsi.md)
### [NFS](sql-server-linux-shared-disk-cluster-configure-nfs.md)
### [SMB](sql-server-linux-shared-disk-cluster-configure-smb.md)

# 概念
## Install
### [安装 SQL Server](sql-server-linux-setup.md)
### [安装 SQL Server 工具](sql-server-linux-setup-tools.md)
### [安装 SQL Server 代理](sql-server-linux-setup-sql-agent.md)
### [安装 SQL Server 全文搜索](sql-server-linux-setup-full-text-search.md)
### [安装 SQL Server Integration Services](sql-server-linux-setup-ssis.md)
### [注册 GA 存储库](sql-server-linux-change-repo.md)

## 配置
### [使用 mssql conf 配置](sql-server-linux-configure-mssql-conf.md)
### [环境变量](sql-server-linux-configure-environment-variables.md)
### [配置 Docker 容器](sql-server-linux-configure-docker.md)
### [客户反馈](sql-server-linux-customer-feedback.md)

## [开发](sql-server-linux-develop-overview.md)
### [连接库](sql-server-linux-develop-connectivity-libraries.md)
### [使用 Visual Studio Code](sql-server-linux-develop-use-vscode.md)
### [使用 SSMS](sql-server-linux-develop-use-ssms.md)
### [使用 SSDT](sql-server-linux-develop-use-ssdt.md)

## [管理](sql-server-linux-management-overview.md)
### [使用 SSMS 进行管理](sql-server-linux-manage-ssms.md)
### [使用 PowerShell 进行管理](sql-server-linux-manage-powershell.md)
### [使用日志传送](sql-server-linux-use-log-shipping.md)
### [使用 DB 邮件和电子邮件警报](sql-server-linux-db-mail-sql-agent.md)

## [迁移](sql-server-linux-migrate-overview.md)
### [从 Windows 导出和导入 BACPAC](sql-server-linux-migrate-ssms.md)
### [使用 SQL Server 迁移助手进行迁移](sql-server-linux-migrate-ssma.md)
### [使用 bcp 批量复制](sql-server-linux-migrate-bcp.md)

## [提取、转换和加载](sql-server-linux-migrate-ssis.md)
### [限制和已知问题](sql-server-linux-ssis-known-issues.md)
### [配置 SSIS](sql-server-linux-configure-ssis.md)
### [计划 SSIS 包](sql-server-linux-schedule-ssis-packages.md)

## [配置业务连续性](sql-server-linux-business-continuity-dr.md)
### [备份和还原](sql-server-linux-backup-and-restore-database.md)
#### [虚拟设备接口 - Linux](sql-server-linux-backup-vdi-specification.md)
### [故障转移群集实例](sql-server-linux-shared-disk-cluster-concepts.md)
#### [Red Hat Enterprise Linux]()
##### [配置（HA 加载项）](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)
##### [操作（HA 加载项）](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
#### [SUSE Linux Enterprise Server]()
##### [配置（HA 加载项）](sql-server-linux-shared-disk-cluster-sles-configure.md)
### [可用性组](sql-server-linux-availability-group-overview.md)
#### [针对高可用性创建](sql-server-linux-availability-group-ha.md)
##### [配置 AG](sql-server-linux-availability-group-configure-ha.md)
##### [在 RHEL 上配置](sql-server-linux-availability-group-cluster-rhel.md)
##### [在 SUSE 上配置](sql-server-linux-availability-group-cluster-sles.md)
##### [在 Ubuntu 上配置](sql-server-linux-availability-group-cluster-ubuntu.md)
##### [操作](sql-server-linux-availability-group-failover-ha.md)
#### [仅为读取缩放创建]()
##### [配置 AG](sql-server-linux-availability-group-configure-rs.md)

## [安全性](sql-server-linux-security-overview.md)
### [开始使用安全功能](sql-server-linux-security-get-started.md)
### [加密连接](sql-server-linux-encrypted-connections.md)

## 性能
### [最佳做法](sql-server-linux-performance-best-practices.md)
### [开始使用性能功能](sql-server-linux-performance-get-started.md)

# 示例
## 无人参与安装
### [Red Hat Enterprise Linux](sample-unattended-install-redhat.md)
### [SUSE Linux Enterprise Server](sample-unattended-install-suse.md)
### [Ubuntu](sample-unattended-install-ubuntu.md)

# Resources
## [故障排除](sql-server-linux-troubleshooting-guide.md)
## [SQL Server 文档](../sql-server/sql-server-technical-documentation.md)
## 伙伴
### [监视](../sql-server/partner-monitor-sql-server.md)
### [高可用性和灾难恢复](../sql-server/partner-hadr-sql-server.md)
### [管理](../sql-server/partner-management-sql-server.md)
### [开发](../sql-server/partner-dev-sql-server.md)
## [DBA Stack Exchange](https://dba.stackexchange.com/questions/tagged/sql-server)
## [Stack Overflow](http://stackoverflow.com/questions/tagged/sql-server)
## [MSDN 论坛](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver)
## [Microsoft Connect](https://connect.microsoft.com/SQLServer/Feedback)
## [Reddit](https://www.reddit.com/r/SQLServer)
