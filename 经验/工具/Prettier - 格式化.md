[官网]()
有多种层面的存在：node pkg、IDE扩展：在编辑中format、Git Hooks在提交时、ESLint Plugin：搭配ESLint
## node 包
在项目中引入prettier，有两个配置文件：`.prettierrc.json` & `.prettierignore`
### .prettierrc.json
配置规则
### .prettierignore
忽略特定文件和目录
## VSCode 插件
在IDE中使用prettier
配置项：默认格式化方式
格式化可以通过快捷键触发或保存时自动进行。
## Git Hooks
## eslint-plugin-prettier
[prettier/eslint-plugin-prettier: ESLint plugin for Prettier formatting (github.com)](https://github.com/prettier/eslint-plugin-prettier)
这是prettier为ESLint推出的插件，通过ESLint使用prettier格式化，格式化的信息通过ESLint抛出。

往往还需要配合[prettier/eslint-config-prettier: Turns off all rules that are unnecessary or might conflict with Prettier. (github.com)](https://github.com/prettier/eslint-config-prettier)使用

	反过来，也有eslint作为prettier的插件：[prettier-eslint](https://github.com/prettier/prettier-eslint)，这同样是prettier自己推出的
### eslint-config-prettier
#### Reference
[使用 prettier 统一代码格式化 - 掘金 (juejin.cn)](https://juejin.cn/post/7202896198608863269?searchId=20230907094808A478F28A8D5534FFC29B#heading-9)