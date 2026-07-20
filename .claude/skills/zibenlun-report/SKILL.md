---
name: zibenlun-report
description: 创作「重读马克思」系列下一篇报告。生成 reports/ 下编号 Markdown + docs/ 下全新视觉风格的排版 HTML，更新首页与 README，自动提交并推送（GitHub 连不上时走 127.0.0.1:10808 代理）。用户说"继续下一篇"/指定选题时使用。
---

# 重读马克思 · 新篇创作流程

用户调用本 skill 时，可能给出选题（如"利润率趋向下降与行业内卷"），也可能只说"继续下一篇"。按以下步骤执行。

## 第 0 步：确定篇目

1. `ls reports/` 确定下一篇编号 NN（最大编号 + 1）。
2. 选题：用户指定则用之；否则从候选池推荐一个并确认：
   - 劳动力再生产与教育内卷/学历贬值（第一卷·劳动力价值）
   - 协作与分工：远程办公与众包（第一卷·第11、12章）
   - 免费劳动与 UGC：用户生产内容（第一卷）
   - 货币、通胀与数字货币（第一卷·第3章）
   - 信用与股份资本：从郁金香到加密货币（第三卷）
   - 绝对/相对剩余价值在服务业（第一卷·第10章）

## 第 1 步：写 Markdown 源文件 → `reports/NN-中文标题.md`

先读最近一篇（如 `reports/11-利润率趋向下降与行业内卷.md`）校准文风。固定结构：

1. `# emoji 标题` + 副标题引文 + 元信息行（理论基础注明《资本论》卷次章节 + 当天日期）
2. `> [!NOTE]` 核心论点
3. `## 一、引言`（2026 年当代现象切入）+ `> [!IMPORTANT]` 问题的提出（先破主流解释）
4. `## 二、理论基石`（分小节讲透对应章节，引《资本论》原文 blockquote + 出处行；至少一个 `> [!WARNING]` 纠正常见误读）
5. `## 三、一张表：19世纪 × 21世纪`（加粗维度列）
6. `## 四、解剖XX`（开头用 `> [!NOTE]` 写明与系列前篇的递进关系；分 3-4 个小节，行文自然"呼应第N篇"）
7. `## 五、超越马克思：XX的三个新特征`（表格）
8. `## 六、结论`：核心发现（编号列表）→ 出路（表格：制度/分配/工时/观念）→ `> [!TIP]` 国际镜鉴 → 马克思的启示（引文）→ `> [!TIP]` 最后的判断（加粗核心句收尾）
9. 末尾分隔线 + 斜体报告生成时间行

要求：理论准确，引文用通行中译本；每篇与系列前篇至少 3 处显式"呼应"；口语化概念（内卷、种草）必须还原为政治经济学范畴。

## 第 2 步：写排版 HTML → `docs/english-slug.html`

**风格必须每篇不同。** 先扫一遍现有 `docs/*.html` 的 `<title>` 和背景，确认已用风格；禁止重复。已用风格登记（新篇完成后追加）：

| 篇 | 文件 | 风格 |
|---|---|---|
| 01 | labor-theory-of-value | 深藏青渐变+衬线 |
| 02 | 996-vs-factory-acts | 浅灰底报告风 |
| 03/04/06/07/08 | digital-rent 等 | 紫色渐变卡片风 |
| 05 | financialization | 深蓝金融风 |
| 09/10 | ai-does-not-create-value / commodity-fetishism | 黑底绿字终端风 |
| 11 | profit-rate-fall-involution | 米黄纸张复古报纸/宣言印刷风（红印章、双划线报头） |

备选新风格：学术期刊双栏排版、极简白底大字排版、黑板粉笔风、拼贴杂志风、档案文件风（牛皮纸+打字机字体）、霓虹赛博风——也可自创，与主题契合即可。

HTML 内容与 Markdown 对应转换：`> [!NOTE/IMPORTANT/WARNING/TIP]` → 带标签的提示框组件；blockquote 引文 → 引文组件（保留出处 cite）；表格、公式、代码块按新风格设计。单文件、内联 `<style>`、无外部依赖、含响应式 `@media`。

## 第 3 步：同步两处索引

- `docs/index.html`：在 `.reports` 末尾追加卡片（报告编号 NN、标题、一句 desc、3 个 tag、英文 slug 链接）
- `README.md`：目录表加一行（# / 报告链接 / 核心议题 / 理论基础）；目录结构树两处（reports/ 与 docs/）各加一行

## 第 4 步：提交并推送

```bash
git add reports/NN-*.md docs/<slug>.html docs/index.html README.md .claude/skills/
git commit -m "新增第NN篇：<标题>（<风格名> HTML）"  # 附 Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>
git push
# 若 push 连接 github.com 失败，直接重试：
git -c http.proxy=http://127.0.0.1:10808 -c https.proxy=http://127.0.0.1:10808 push
# 10808 不通再依次试 7890 / 7897 / 10809
```

不要提交 `test.pdf`、`test_pdf.py`、`.claude/settings.local.json` 等无关文件。

## 第 5 步：汇报

简述：篇目与选题理由、核心论点一句话、产出文件列表、本篇 HTML 用了什么新风格、commit hash 与推送结果。
