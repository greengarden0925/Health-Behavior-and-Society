# 維護指南

這個站台用 Markdown 檔寫成，每章一個檔，推到 GitHub 後由 GitHub Actions 自動建置並發布。

## 檔案結構

```text
.
├── mkdocs.yml                 # 站台設定與左側選單
├── requirements.txt           # 建置工具（zensical）
├── .github/workflows/docs.yml # 推送到 main 時自動發布
└── docs/
    ├── index.md               # 首頁（各部分與章節連結）
    ├── usage.md               # 使用說明
    ├── exam-map.md            # 歷屆國考題對照表
    ├── glossary.md            # 名詞全寫
    ├── maintenance.md         # 本頁
    └── chapters/V00.md … V40.md   # 每章一個檔
```

## 本機預覽

```bash
pip install -r requirements.txt
zensical serve        # 開啟 http://localhost:8000，存檔後自動更新
zensical build --clean  # 輸出到 site/，檢查有沒有警告
```

## 修改內容

1. 直接編輯 `docs/chapters/Vxx.md`，提交並推送到 `main`。
2. 約一到兩分鐘後網站更新。
3. 每章第一行用 `# Vxx 章名`，左側選單的章名會取自這一行。

## 新增一章

1. 新增 `docs/chapters/V41.md`。
2. 在 `mkdocs.yml` 的 `nav` 對應的「部分」底下加一行 `- chapters/V41.md`。
3. 在 `docs/index.md` 加一行連結，並在 `docs/exam-map.md` 加上該章列。

## 國考題格式

答案用可收合區塊，學生要先作答再點開。每題照下面格式，注意空行和縮排（四個空格）：

```markdown
**【114 年第 6 題】** 題幹

- (A) 選項一
- (B) 選項二
- (C) 選項三
- (D) 選項四

??? success "查看答案"

    **答案：C**
```

新增年度題目時：

- 題號寫成「年度、第幾題」，並放進該章最後的「歷屆國考題」區。
- 同步更新 `docs/exam-map.md` 的題數與題號。
- 答案以考選部公告為準；公告有更正或多選給分時，在答案後加一句說明。

## 撰寫慣例

- 第一次出現的縮寫要附全寫，例如「一般適應症候群（General Adaptation Syndrome, GAS）」，並補進 `docs/glossary.md`。
- 政策與法規寫最新版，並標示年份。
- 清單前面要空一行，巢狀清單縮排四個空格，否則網頁不會正確分行。
- 教學例（自擬情境）要標示「教學例」，不要寫成考題或政策原文。

## 發布設定（只需做一次）

在 GitHub 的 Settings → Pages，把 Source 設為 **GitHub Actions**。之後每次推送到 `main` 都會自動發布。
