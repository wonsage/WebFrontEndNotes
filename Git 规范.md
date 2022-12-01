远程Git服务（开源）：GitHub、Gitee
自建Git服务（私有、备份）：GitLab
客户端本地管理：Git

## 分支管理和工作流
Git flow 是一种功能驱动式（Feature-driven Development）开发。
长期分支

- **master / main 主分支**：产品分支，只能从release和hotfix分支合并内容，不能在此分支直接修改。
- **develop 开发分支**：所有开发完成但未测试的feature会集中在此分支，等待发版

短期分支：

- **feature 功能开发分支**：一般一个功能点划分一个分支，等待整个功能开发完成后合并到开发分支上
- **release 预发版分支**：预发分支：当需要发布时，我们从develop分支创建一个release分支，然后这个release分支会发布到测试环境进行测试，如果发现问题就在这个分支直接进行修复。发布结束后，这个release分支会合并到develop和master分支，从而保证不会有代码丢失。
- **hotfix 补丁分支**：主要用于紧急修复一些bug，会从master分支上的某一个tag建立，修复结束后再合并到develop和master分支上
## Commit
提供充分的change log。Angular规范使用比较广泛：
```git
<TYPE>(<SCOPE>):<SUBJECT>
 
<BODY>

<FOOTER>
```
- TYPE：
	- feat：新功能、新特性；
	- fix：bugfix，问题修复；
	- refactor：代码重构；
	- docs：文档修改；
	- style：代码格式修改（不是CSS修改）；
	- test：测试用例修改；
	- chore：其他修改，如构建、依赖管理等。
- SCOPE：本次commit 的影响范围。
	- route
	- component
	- utils
	- build
	- ...
- SUBJECT：概述。
- BODY：具体描述。
- FOOTER：备注，如链接。
### Hooks

