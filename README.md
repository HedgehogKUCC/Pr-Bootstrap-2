# 練習 - 後台版型

- [Github Page]()

## 使用 Flex 伸縮特性安排組件

如何排版遇到**內容數量不一致**但又要**兼顧對齊美觀**呢 ?
 
<br>

`<div class="h5">` `<div class="h3">` : 

在 dashboard 中 `h3` `h5` 通常只用來顯示文字大小 , 所以改使用這樣的樣式 .

<br>

`<div class="text-center w-100">` :

因為 `flex` 關係 , 所以 `w-100` 是會扣掉左邊 `Font Awesome` 寬度 , 才顯示的 100% .

<br>

`<div class="display-4">172</div>` : 造成高度不同

但其實 `col-lg-3` 已經有伸長高度 , 只是 `class="card"` 沒有而已 .

所以在 `card` 後面再加上 `h-100` 就可以囉 !

<br>

因為 `card-body` 有設置成 `d-flex` 

所以直接可以使用 `align-items-center` 來達到 ***垂直置中***

<br>

不同裝置下有不同的 `grid` 尺寸 

- `<div class="col-lg-3 col-6">`
- `Font Awesome` `d-none d-sm-block`

`注意 :` Bootstrap 中斷點是 由小到大

<br>

dashboard 空間有限 , 又要放入很多不同內容與資料 , 為了節省空間會將文字縮小一點 !

all.css

```css
html {
	font-size : 14px;
}
```

index.html

```html
		<div class="col-lg-3 col-6">
          <div class="card rounded-0 h-100">
            <div class="card-body d-flex align-items-center">
              <div
                class="far fa-money-bill-alt fa-3x text-secondary mr-2 d-none d-sm-block"
              ></div>
              <div class="text-center w-100">
                <div class="h5">今日營收</div>
                <div class="h3">192,000</div>
              </div>
            </div>
          </div>
        </div>
        <div class="col-lg-3 col-6">
          <div class="card rounded-0">
            <div class="card-body d-flex align-items-center">
              <div
                class="fas fa-users fa-3x text-secondary mr-2 d-none d-sm-block"
              ></div>
              <div class="text-center w-100">
                <div class="h5">會員增加</div>
                <div class="display-4">172</div>
              </div>
            </div>
          </div>
        </div>
```