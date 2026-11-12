# 中文练习课堂 · GitHub Pages 部署包

G7 中文课的两个互动练习，纯静态网页，无需服务器、无需数据库。

| 文件 | 内容 |
|---|---|
| `index.html` | 总入口（导航页） |
| `game.html` | 《节日美食》闯关游戏（翻译 / 问答 / 重组句子，A·B 分层） |
| `writing.html` | 书信写作练习（翻译 / 句型问答 / 写信，含格式检查、语法标记、8 分制评分） |
| `teacher.html` | 老师查看成绩（读取本机浏览器保存的成绩记录） |
| `.nojekyll` | 让 GitHub Pages 按原样提供文件，不做 Jekyll 处理 |

---

## 部署步骤（约 3 分钟）

### 方法一：网页上传（最简单，不用命令行）

1. 登录 GitHub，右上角 **+ → New repository**
2. 仓库名随意，例如 `chinese-practice`；选 **Public**（Pages 需要公开仓库，除非用付费计划）；点 **Create repository**
3. 进入仓库后点 **Add file → Upload files**
4. 把本文件夹里的 **4 个文件全部拖进去**（`index.html`、`game.html`、`writing.html`、`teacher.html`）
   - 注意：`.nojekyll` 是隐藏文件，Mac 上按 `Cmd + Shift + .` 才看得到。看不到也没关系，可以跳过，或按方法二用命令行上传。
5. 点 **Commit changes**
6. 进入仓库 **Settings → Pages**
   - **Source** 选 `Deploy from a branch`
   - **Branch** 选 `main`，目录选 `/ (root)`，点 **Save**
7. 等 1 分钟左右，页面顶部会出现网址，形如：
   `https://你的用户名.github.io/chinese-practice/`
8. 把这个网址发给学生即可（建议再发 `.../writing.html` 作为书信练习的直达链接）

### 方法二：命令行（含隐藏文件，推荐）

```bash
cd github-pages            # 进入本文件夹
git init
git add .
git commit -m "Add Chinese practice site"
git branch -M main
git remote add origin https://github.com/你的用户名/chinese-practice.git
git push -u origin main
```

然后在仓库 **Settings → Pages** 里把 Branch 设为 `main` / `/ (root)` 并保存。

---

## 更新内容

改完文件后重新 commit + push，GitHub Pages 会自动在 1 分钟内更新（有时需强制刷新 Ctrl+F5）。

---

## 使用说明

- **完全静态**：所有判分、评分、语法标记都在浏览器里完成，不联网也能用（也可直接双击 `index.html` 在本地打开）。
- **成绩保存在哪里**：存在学生所用浏览器的 localStorage 里。同一台设备上打开 `teacher.html` 就能看到该设备产生的全部记录（姓名、时间、各关得分、写作等级与信件全文）。学生换设备或清除浏览器数据，记录不会跟着走。
- **跨设备收集成绩**：让学生做完点「📋 复制我的成绩（发给老师）」，把文字粘贴发到邮件 / Teams / 微信，最稳妥。
- **注意**：`file://` 直接打开时，剪贴板复制功能可能被浏览器限制；用 GitHub Pages 的 https 网址访问则完全正常。

## 自定义

- 改题目：打开对应 html，搜索 `const DATA = {`（game.html）或 `const TR = [` / `const QA = [`（writing.html），按格式增删条目即可。
- 改写作评分规则：`writing.html` 里的 `FORMAT_PARTS`（格式六要素）、`PATTERNS`（句型）、`GRAMMAR_RULES`（语法检查）、`gradeEssay()` 里的等级换算。
- 仓库名、标题、学校名称在 `index.html` 里修改。
