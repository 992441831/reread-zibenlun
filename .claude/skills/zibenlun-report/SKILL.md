---
name: zibenlun-report
description: 创作「重读马克思」系列下一篇报告。生成 reports/ 下编号 Markdown + docs/ 下全新视觉风格的排版 HTML，更新首页与 README，自动提交并推送（含 .claude/settings.local.json；GitHub 连不上时走 127.0.0.1:10808 代理）。用户说"继续下一篇"/指定选题时使用。
---

# 重读马克思 · 新篇创作流程

用户调用本 skill 时，可能给出选题（如"利润率趋向下降与行业内卷"），也可能只说"继续下一篇"。按以下步骤执行。**全流程一次做完，包括提交与推送，不要中途停下来等确认。**

## 第 0 步：确定篇目

1. `ls reports/` 确定下一篇编号 NN（最大编号 + 1）。
2. 选题：用户指定则用之；否则从候选池推荐一个并确认：
   - 免费劳动与 UGC：用户生产内容（第一卷）
   - 信用与股份资本：从郁金香到加密货币（第三卷）
   - 绝对/相对剩余价值在服务业（第一卷·第10章）
3. 选题定后，**立即从本文件候选池中划掉该题**（连同新增候选可补充），与其他文件一并提交。

## 第 1 步：写 Markdown 源文件 → `reports/NN-中文标题.md`

先读最近一篇（如 `reports/14-货币与数字货币.md`）校准文风。固定结构：

1. `# emoji 标题` + 副标题引文 + 元信息行（理论基础注明《资本论》卷次章节 + 当天日期）
2. `> [!NOTE]` 核心论点
3. `## 一、引言`（当代现象切入）+ `> [!IMPORTANT]` 问题的提出（先破主流解释）
4. `## 二、理论基石`（分小节讲透对应章节，引《资本论》原文 blockquote + 出处行；至少一个 `> [!WARNING]` 纠正常见误读）
5. `## 三、一张表：19世纪 × 21世纪`（加粗维度列）
6. `## 四、解剖XX`（开头用 `> [!NOTE]` 写明与系列前篇的递进关系；分 3-4 个小节，行文自然"呼应第N篇"）
7. `## 五、超越马克思：XX的三个新特征`（表格）
8. `## 六、结论`：核心发现（编号列表）→ 出路（表格：制度/分配/工时/观念）→ `> [!TIP]` 国际镜鉴 → 马克思的启示（引文）→ `> [!TIP]` 最后的判断（加粗核心句收尾）
9. 末尾分隔线 + 斜体报告生成时间行

要求：理论准确，引文用通行中译本；每篇与系列前篇至少 3 处显式"呼应"；口语化概念（内卷、种草）必须还原为政治经济学范畴。

## 第 2 步：写排版 HTML → `docs/english-slug.html`

**风格必须每篇不同。** 先看下表登记，禁止重复；写完后把本篇风格追加进表。

| 篇 | 文件 | 风格 |
|---|---|---|
| 01 | labor-theory-of-value | 深藏青渐变+衬线 |
| 02 | 996-vs-factory-acts | 浅灰底报告风 |
| 03/04/06/07/08 | digital-rent 等 | 紫色渐变卡片风 |
| 05 | financialization | 深蓝金融风 |
| 09/10 | ai-does-not-create-value / commodity-fetishism | 黑底绿字终端风 |
| 11 | profit-rate-fall-involution | 米黄纸张复古报纸/宣言印刷风（红印章、双划线报头） |
| 12 | education-involution | 学术期刊论文风（白底、摘要框、关键词、三线表、卷期页眉） |
| 13 | cooperation-division-of-labor | 黑板粉笔风（深绿黑板+木框、粉笔黄蓝粉、虚线板书框、课堂讲授口吻） |
| 14 | money-and-digital-currency | 钞票/银行券风（米绿券面、扭索纹双线边框、四角券号、圆形面值章、凹印铭文引文） |

备选新风格：极简白底大字排版、拼贴杂志风、档案文件风（牛皮纸+打字机字体）、霓虹赛博风、手稿批注风、蓝图工程图风——也可自创，与主题契合（拟物化优先：本篇主题是什么物件，就做成什么物件的样子）。

HTML 内容与 Markdown 对应转换：`> [!NOTE/IMPORTANT/WARNING/TIP]` → 带标签的提示框组件（"系列递进"框必须保留）；blockquote 引文 → 引文组件（保留出处 cite）；表格、公式、代码块按新风格设计。单文件、内联 `<style>`、无外部依赖、含响应式 `@media`。

**写完 HTML 自查（逐项过一遍再提交）：**
- [ ] CSS 无笔误/无效行（历史教训：13 篇曾混入 `background: #1a2venue;` 残行）
- [ ] Markdown 的每个章节、提示框、表格都在 HTML 中有对应（允许按风格改写措辞，不允许漏内容块）
- [ ] 标题/日期/理论基础卷次与 md 一致；slug 与 index.html 卡片链接一致

## 第 3 步：同步两处索引

- `docs/index.html`：在 `.reports` 末尾追加卡片（报告编号 NN、标题、一句 desc、3 个 tag、英文 slug 链接）
- `README.md`：目录表加一行（# / 报告链接 / 核心议题 / 理论基础）；目录结构树两处（reports/ 与 docs/）各加一行

## 第 4 步：提交并推送

```bash
git add reports/NN-*.md docs/<slug>.html docs/index.html README.md .claude/
git commit -m "新增第NN篇：<标题>（<风格名> HTML）"  # 附 Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>
git push || git -c http.proxy=http://127.0.0.1:10808 -c https.proxy=http://127.0.0.1:10808 push
# 10808 不通再依次试 7890 / 7897 / 10809
```

说明：`.claude/` 整个目录纳入提交（含 skill 更新与 `settings.local.json` 的权限配置变更——用户要求一并纳入版本管理）。**不要提交** `test.pdf`、`test_pdf.py` 及其他与本篇无关的未跟踪文件。

## 第 5 步：收尾

1. 更新持久记忆 `memory/reread-zibenlun-series-conventions.md`：进度（已写到第NN篇）与已用风格列表。
2. 向用户汇报：篇目与选题理由、核心论点一句话、产出文件列表、本篇 HTML 用了什么新风格、commit hash 与推送结果（直连成功还是走了代理）。
