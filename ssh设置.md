### 用户文件夹ssh配置文件新增内容
```powershell
Host github-seeklaw
  Hostname ssh.github.com
  Port 443
  User git
  IdentityFile A:\ssh_pushKEY\seeklaw\1\sshKey1
  IdentitiesOnly yes
```
### 仓库目录终端输出结果
```powershell
Windows PowerShell
版权所有（C） Microsoft Corporation。保留所有权利。

安装最新的 PowerShell，了解新功能和改进！https://aka.ms/PSWindows

PS G:\pc_back\2025-11-30\E\robo\ropo-seeklaw> git log
fatal: detected dubious ownership in repository at 'G:/pc_back/2025-11-30/E/robo/ropo-seeklaw'
'G:/pc_back/2025-11-30/E/robo/ropo-seeklaw' is owned by:
        NT AUTHORITY/SYSTEM (S-1-5-18)
but the current user is:
        SEEKLAW/seekl (S-1-5-21-634308478-3152111761-1455805516-1001)
To add an exception for this directory, call:

        git config --global --add safe.directory G:/pc_back/2025-11-30/E/robo/ropo-seeklaw
PS G:\pc_back\2025-11-30\E\robo\ropo-seeklaw> git config --global --add safe.directory G:/pc_back/2025-11-30/E/robo/ropo-seeklaw
PS G:\pc_back\2025-11-30\E\robo\ropo-seeklaw> git log
commit 78ea9669fd6b37913188ebec4f555f17462c0f8d (HEAD -> main, origin/main)
Author: seeklaw <seeklaw@outlook.com>
Date:   Mon Nov 10 11:09:19 2025 +0800

    repo init
PS G:\pc_back\2025-11-30\E\robo\ropo-seeklaw> git remote -v
origin  git@github.com:seeklaw/seeklaw.github.io.git (fetch)
origin  git@github.com:seeklaw/seeklaw.github.io.git (push)
PS G:\pc_back\2025-11-30\E\robo\ropo-seeklaw> git config --local user.signingkey
22210994F0C3002B2186221C17AC3B991589770C
PS G:\pc_back\2025-11-30\E\robo\ropo-seeklaw> git config --local user.signingkey C546F9C48CC823815AFA6432D47C8CDEA6246555
PS G:\pc_back\2025-11-30\E\robo\ropo-seeklaw> git config --local user.signingkey
C546F9C48CC823815AFA6432D47C8CDEA6246555
PS G:\pc_back\2025-11-30\E\robo\ropo-seeklaw> git remote set-url origin git@github-seeklaw:seeklaw/seeklaw.github.io.git
PS G:\pc_back\2025-11-30\E\robo\ropo-seeklaw> git remote -v
origin  git@github-seeklaw:seeklaw/seeklaw.github.io.git (fetch)
origin  git@github-seeklaw:seeklaw/seeklaw.github.io.git (push)
PS G:\pc_back\2025-11-30\E\robo\ropo-seeklaw> ssh -T git@github-seeklaw
Bad permissions. Try removing permissions for user: NT AUTHORITY\\Authenticated Users (S-1-5-11) on file A:/ssh_pushKEY/seeklaw/1/sshKey1.
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions for 'A:\\ssh_pushKEY\\seeklaw\\1\\sshKey1' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
Load key "A:\\ssh_pushKEY\\seeklaw\\1\\sshKey1": bad permissions
git@ssh.github.com: Permission denied (publickey).
PS G:\pc_back\2025-11-30\E\robo\ropo-seeklaw>

```
### 终端管理员输出结果
```powershell
Windows PowerShell
版权所有（C） Microsoft Corporation。保留所有权利。

安装最新的 PowerShell，了解新功能和改进！https://aka.ms/PSWindows

PS C:\Users\seekl> cd A:\ssh_pushKEY\seeklaw\1
PS A:\ssh_pushKEY\seeklaw\1> icacls "A:\ssh_pushKEY\seeklaw\1\sshKey1" /inheritance:r
已处理的文件: A:\ssh_pushKEY\seeklaw\1\sshKey1
已成功处理 1 个文件; 处理 0 个文件时失败
PS A:\ssh_pushKEY\seeklaw\1> icacls "A:\ssh_pushKEY\seeklaw\1\sshKey1" /grant "%USERNAME%":F
无效参数“%USERNAME%”
PS A:\ssh_pushKEY\seeklaw\1> icacls "A:\ssh_pushKEY\seeklaw\1\sshKey1" /remove "Authenticated Users" "Everyone" "Users"
已处理的文件: A:\ssh_pushKEY\seeklaw\1\sshKey1
已成功处理 1 个文件; 处理 0 个文件时失败
PS A:\ssh_pushKEY\seeklaw\1> ssh -T git@github-seeklaw
Load key "A:\\ssh_pushKEY\\seeklaw\\1\\sshKey1": Permission denied
git@ssh.github.com: Permission denied (publickey).
PS A:\ssh_pushKEY\seeklaw\1> icacls "A:\ssh_pushKEY\seeklaw\1\sshKey1" /grant "$($env:USERNAME):F"
已处理的文件: A:\ssh_pushKEY\seeklaw\1\sshKey1
已成功处理 1 个文件; 处理 0 个文件时失败
PS A:\ssh_pushKEY\seeklaw\1> icacls "A:\ssh_pushKEY\seeklaw\1\sshKey1"
A:\ssh_pushKEY\seeklaw\1\sshKey1 SEEKLAW\seekl:(F)

已成功处理 1 个文件; 处理 0 个文件时失败
PS A:\ssh_pushKEY\seeklaw\1> ssh -T git@github-seeklaw
Enter passphrase for key 'A:\ssh_pushKEY\seeklaw\1\sshKey1':
Hi seeklaw! You've successfully authenticated, but GitHub does not provide shell access.
PS A:\ssh_pushKEY\seeklaw\1>
```