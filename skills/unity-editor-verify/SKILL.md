---
name: unity-editor-verify
description: 用命令行触发 Unity 编辑器任务（场景重建 / 冒烟测试 / HUD 校验）并核验 PASS 证据时使用，含 GUI 模式启动、License 抖动处理、进程等待与证据核验流程
---

# Unity 编辑器命令验收

## 何时触发

- 一次 Unity stage run 需要声称「场景已重建 / 编译通过 / 冒烟测试全绿 / HUD 校验通过」
- 需要在命令行用 `-executeMethod` 跑编辑器方法，并拿到可核验的证据

## 输入

1. 入口方法（分场景重建 / 冒烟测试 / HUD 校验三类）
2. 日志输出路径、上一次基线报告的时间戳
3. 工程路径与引擎路径（`-projectPath`、`Unity.exe`）

## 步骤

1. **GUI 模式启动，不要加 `-quit`**——入口方法自己会调 `EditorApplication.Exit`：

   ```
   Unity.exe -projectPath <proj> -executeMethod <Namespace.Method> -logFile <log>
   ```

2. **License 抖动不算失败**：日志出现 entitlement 404、`Account API did not become accessible within 30 seconds` 这类握手错误时，杀掉 Unity 主进程与 AssetImportWorker 进程，重跑同一条命令。成功标志是日志出现 `Successfully resolved entitlement details`。

3. **直接调用会先返回**：用 `Get-CimInstance Win32_Process -Filter "Name = 'Unity.exe'"` 拿 PID，再 `Wait-Process -Id <pid> -Timeout 180` 等它真正结束。

4. **只信证据，不看退出码**：
   - 报告文件时间戳晚于本次启动时间
   - 报告尾部有 `FAILED count: 0`
   - 编辑器日志里没有 `error CS`、没有未捕获异常
   - 结束时没有残留 Unity 进程

5. **截图复核可选**：需要看画面时把渲染截图交给视觉模型判读，但结论以日志与报告为准，不以截图为准。

## 验收

- [ ] 报告时间戳新于本次运行
- [ ] `FAILED count: 0`
- [ ] 无编译错误、无未捕获异常
- [ ] Unity 进程已退出

## 坑

- 工程目录可能不是 git 仓库，别用 `git status` 判断状态。
- 只跑了一半的任务也会生成报告，**必须看尾部统计行**，不能看到文件存在就宣布通过。
- 同一份日志重复追加时，时间戳会骗人；先确认日志被截断/新建。
