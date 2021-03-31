---
title: '利用 GitHub Action 自動部署 Hugo 部落格'
date: 2021-03-31T11:17:50+08:00
draft: false
categories: ['hugo']
---
![](/img/tg_image_519956313.jpeg)
# 在 GitHub 建立 Repo
註冊並登入 GitHub 後，點右上角的 New Repository，並填寫 Repo 名稱等資訊便可建立 Repo。
# 上傳部落格原始碼
對於剛使用 GitHub 的新手，最簡單的方式是將部落格原始碼直接拖拉到你的儲存庫頁面便可完成上傳。

你也可以使用 Git 客戶端來上傳，這會讓未來新增文章時更加方便。
# 建立 Workflow
新增 `.github/workflows/build.yaml` 檔案並填入下方的資料即可建立 Workflow 了，每次當你推送 commit 時，GitHub 會幫你自動部署到 Github Pages 上頭。

```yaml
name: Github-Pages

on:
  push:
    branches:
      - main #你的 branch 名稱
jobs:
  deploy:
    runs-on: ubuntu-18.04
    steps:
      - uses: actions/checkout@v1
        with:
          submodules: true
      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: '0.81.0' # hugo 版本，建議填寫與你電腦相符的版本
          extended: true
      - name: Build
        run: hugo --gc --minify --cleanDestinationDir
      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_branch: public
          publish_dir: ./public
          force_orphan: true
          #cname: aaa.bbb.com # 你的網域名稱，填寫此項便會自動建立 CNAME 檔案（注意：你必須將 DNS 記錄指向 GitHub Pages）
```
# 設定 GutHub Pages
![](/img/tg_image_244516670.jpeg)

在填寫完成 workflow 後，如果沒出差錯的話你部署完成的部落格應該會在 public 分支（branch）

接下來僅需幾個步驟即可讓部落格上線！

在 Repo 頁面的上方標前欄中選擇 Settings 在下面你可以找到 GitHub Pages 區塊。

- Source: 選擇 public
- Custom domain: 若你想放在自訂域名上你要填寫這項，並參考 [Configuring a custom domain for your GitHub Pages site](https://docs.github.com/en/github/working-with-github-pages/configuring-a-custom-domain-for-your-github-pages-site) 來設定你域名的 DNS

都填好後按下 Save 你的部落格就正式上線了！