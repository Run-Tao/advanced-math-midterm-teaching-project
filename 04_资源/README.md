# 04_资源 · 资源清单与来源

> 本目录是项目的**唯一资源入口**。`Source/` 与 `Downloads/` 保持同级，使 `align_share_bookmarks.py` 里的 `../Downloads/` 相对路径可直接工作——项目不依赖本文件夹之外的任何路径。

## 1. 目录结构

```
04_资源/
├── README.md                ← 本文件
├── Source/                  可复现源码（LaTeX + 生成/复核脚本 + 题库）
├── Downloads/               成品 PDF
├── 复核/                    四册题库的既有答案复核脚本
└── 参考/                    真题考点索引
```

## 2. Downloads（成品）

| 文件 | 说明 |
| --- | --- |
| `讲义_高数I期中_分享版_2026-11-09.pdf` | **主讲义**：31 页 / 48 书签 / 8 章 + 5 附录 / 33 道例题精讲 + 151 道章末习题 |
| `新讲义起手式_tlnote_11-09.pdf` | 1 页排版样板，展示 `tlnote.sty` 的语义盒与命令契约，供维护讲义时对照 |

## 3. Source（可复现源码）

| 文件 | 职责 |
| --- | --- |
| `讲义_高数I期中_分享版.tex` | 生成出的讲义 LaTeX 成品源（**不要手改**，改 `_share_notes.tex`） |
| `_share_notes.tex` | 8 章讲解 + 卷首 + 5 附录的内容源，按 `%%FRONT%%` / `%%CH1..8%%` / `%%BACK%%` 分段 |
| `verify_share_handout.py` | 33 道例题答案独立复核，sympy + mpmath，PASS 82 / FAIL 0 |
| `build_share_handout.py` | 装配讲义；两道硬闸门（复核全绿 + 151 题配对 / 8 章映射 / 33 例题 / 环境配对） |
| `align_share_bookmarks.py` | 以 `.toc` 为真值对齐 PDF 书签，并把成品归档到 `../Downloads/` |
| `_build_compact_handout.py` | 题库解析器（题面 / 答案 / 章节映射）。生成器把 `SRC` 覆盖为当前目录 |
| `_新讲义起手式_tlnote.tex` | 新讲义起手式，记录模板约定与「禁止重复定义」清单 |
| `讲义_泰勒与压轴强化_11-08.tex` | 题库册一（19 题，T 组） |
| `讲义_全专题冲顶_11-08.tex` + `part2_body.tex` | 题库册二（62 题，S 组；须两文件同目录） |
| `讲义_加练_定义与压轴深化_11-08.tex` | 题库册三（40 题，P 组） |
| `讲义_网络对标加练_11-08.tex` | 题库册四（30 题，W 组） |

四册合计 **151 题**，题面与答案已配对，答案由 `复核/` 下脚本锁定。

## 4. 复核（答案背书）

| 文件 | 覆盖 | 结果 |
| --- | --- | --- |
| `verify_taylor_drill.py` | 册一 19 题 + 限时卷 12 题 + 母函数表 | PASS 58 / FAIL 0 |
| `verify_full_topics_drill.py` | 册二 62 题 + 模拟卷 A/B 各 18 题 | PASS 154 / FAIL 0 |
| `verify_extra_drill.py` | 册三 40 题 + 模拟卷 C 18 题 | PASS 106 / FAIL 0 |
| `verify_web_drill.py` | 册四 30 题（含 6000 次高精度迭代） | PASS 78 / FAIL 0 |

> 这四个脚本是**答案正确性的背书**，不参与讲义生成链；改动题库答案后应先跑对应脚本。

## 5. 参考

| 文件 | 说明 |
| --- | --- |
| `真题考点索引_2008-2025.md` | 十七套高数 A 类期中真题的试卷骨架、必考频次、第 11 题形式分布与逐卷建议 |

> 该文件正文里的 `D:\Run_Tao\Homework\...` 是**原稿出处标注**，不是本项目的运行依赖；本项目不使用这些路径。

## 6. 复现命令

```bash
cd "04_资源/Source"
PYTHONIOENCODING=utf-8 python verify_share_handout.py       # PASS 82 / FAIL 0
PYTHONIOENCODING=utf-8 python build_share_handout.py        # 生成 .tex
xelatex -interaction=nonstopmode -halt-on-error 讲义_高数I期中_分享版.tex   # 迭代至 .toc/.out 稳定
PYTHONIOENCODING=utf-8 python align_share_bookmarks.py     # 书签对齐 + 归档到 ../Downloads/
```

环境依赖（工具，不是项目内容）：XeLaTeX、已安装的 `tlnote.sty`、Python 的 `sympy` / `mpmath` / `pymupdf`。

## 7. 来源与边界

- 本目录文件是 `Note` 仓库中高数期中材料与 `Homework` 模板工程的**同步副本**，便于本独立项目自包含使用；副本与源仓库不做自动同步，改动以本目录为准。
- 讲义答案由脚本复核后写入，**不接受手改答案**；改内容请走 §6 全流程。
- **不含真题卷面原件**（U12）；需要卷面请通过学校渠道获取。
- 待补充（U15）：课件、视频、板书照片等其它配套资源未提供，可按需在 `04_资源/` 下新建子目录并在本文件登记。
