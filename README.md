# 在 next 中使用 Adobe Animate Canvas
使用 [Next.js](https://nextjs.org/) 專案，使用 [`create-next-app`](https://github.com/vercel/next.js/tree/canary/packages/create-next-app) 建置專案。

## 開始專案

1. 用以下的指令跑專案

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev
```
2. 其他的知識請參考 create-next-app

## 安裝套件
1. 使用了 Sass
2. 使用了 Bootstrap Container

## 將 Adobe Animate 產出的內容置放在專案中
1. 將產出的畫及繪圖資源放進 public 當中，應該會有 .js 或 images 資料夾
2. 將產出的 index.html 打開
3. 重點是如何將 index.html 的內容搬到你要的頁面，像是目前這範例的 animate.jsx 裡
4. index.html 中的 HTML 部份，目前搬到 animate.jsx 中的 <main> 中，原來寫在上面的 style 屬性的樣式，全都搬到 Animate.module.sass 中
5. index.html 中的 function init 和 handleComplete，也搬進去 animate.jsx 裡
6. 在 index.html 中用 var 宣告的變數，也搬到 animate.jsx 中在一堆 useState 下用 let 宣告了一次
7. 比較特別的是原本有 var 一個 stage 的變數，這個拿掉，因為會和 window 的 stage 屬性衝突，所以這個變數會直接用 window.stage1 取代，不用宣告直接用
8. 因為變數改成了 stage1，所以在你產出的動畫的 js 中，用到 stage 變數的，要通通改成 stage1
9. 要注意，不要一口氣用程式搜尋再取代，因為像大寫的 Stage 就不是取代的對象，getStage 也不是取代的對象，stageChild 也不是取代的對象
10. 原本在 html 檔中載入的兩支 JS 檔，變成用 Script 標籤專入，並且是分次載入，兩支都載入後才觸發 init
11. 如果動畫有用到全域變數的，或全域方法的，通通丟到產出的動畫的 js 檔的最前面，參考 public 下的 cake.js
12. [部置的測試網站](https://next-adobe-animate-01.vercel.app/)