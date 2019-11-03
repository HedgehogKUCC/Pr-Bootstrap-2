# 練習 - 後台版型

- [Github Page]()

<br>

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

***Dashboard*** 空間有限 , 又要放入很多不同內容與資料 , 為了節省空間會將文字縮小一點 !

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

<br>

## Add Chart.js

*選擇 Chart 的要點*

1. 有沒有符合需求的圖表類型
2. 資料結構是否易懂或易於變化
3. 有沒有要支援 Responsive
4. 授權

授權部分像是 [highcharts](https://www.highcharts.com/) 本身免費 , 但要用於商業用途就需要 `license` !

`Chart.js` 的標籤一定要使用 `canvas` 才可以

```html
<canvas id="barCanvas"></canvas>
<canvas class="chart-item"></canvas>
```

<br>

### 巢狀 Grid

```html
<div class="row align-items-end">
	<div class="col-lg-8">
		<div class="row">
			<div class="col-lg-8 align-self-end"></div>
			<div class="col-lg-4"></div>
		</div>
	</div>
	<div class="col-lg-4"></div>
</div>
```

<hr>

`Flex 外容器屬性`

- display
- flex-flow
	- flex-direction
	- flex-wrap
- justify-content
- align-items

<hr>

`Flex 內元件屬性`

- flex
	- flex-grow
	- flex-shrink
	- flex-basis
- order
- align-self

[圖解 - Flex](https://wcc723.github.io/css/2017/07/21/css-flex/)

<br>

### Bootstrap - Components - Progress

[Progress](https://getbootstrap.com/docs/4.3/components/progress/)

<br>

## 表格結構注意細節

### sr-only

只有螢幕閱讀器的人會知道有月份

如果不是的話就會被隱藏但保有它的功能

```html
<label for="month" class="sr-only">月份</label>
```

<br>

### Flex

外層使用 `d-flex` 包住兩個區塊 `form-inline` `button`

因為 `flex` 關係 , 就可以將兩個 `button` 使用 `ml-auto` 移到最右邊 .

#### Dashboard 節省空間

`form-control-sm` `btn-sm`

```html
		   <div class="d-flex mb-4">
            <div class="form-inline">
              <div class="form-group">
                <label for="month" class="sr-only">月份</label>
                <select
                  name="month"
                  id="month"
                  class="form-control form-control-sm"
                >
                  <option value="...">... 月</option>
                </select>
              </div>
            </div>
            <div class="ml-auto">
              <a href="#" class="btn btn-outline-secondary btn-sm">下載報表</a>
              <a href="#" class="btn btn-outline-secondary btn-sm">訂單管理</a>
            </div>
          </div>
```

<br>

### table 結構

`th` 有幾個 `td` 就要有幾個 !!!

不然就要使用 `colspan` 合併儲存格

```html
<table class="table">
	<thead>
		<tr>
			<th>...</th>*7
			...
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>...</td>*7
			...
		</tr>
	</tbody>
	<tfoot>
		<tr>
			<td colspan="6">...</td>
			<td>...</td>
		</tr>
	</tfoot>
</table>
```

<br>

有關 `金額` 都要對齊右邊

*欄位寬度*

- 彈性百分比 (%)
- 固定寬度 (px)

建議

先將 `固定寬度` 設定出來 , 彈性就不用讓它自適應 .

寫在 `th` 表格就會全部套用上

ex :

```html
<thead>
	<tr>
		<th width="50">日期</th>
		<th>訂單數</th>
		<th>退費數</th>
		<th>出貨數</th>
		<th>有問題貨品</th>
		<th width="150">營業額</th>
		<th width="150">淨利潤</th>
	</tr>
</thead>
```

### Responsive table

[v4.3](https://getbootstrap.com/docs/4.3/content/tables/#responsive-tables)

可解決 `table` 在比較小的螢幕裝置下 , 會自動產生 `x軸` 水平捲動 .

```html
<div class="table-responsive">
  <table class="table">
    ...
  </table>
</div>
```

<br>

## Tooltips

[Tooltips](https://getbootstrap.com/docs/4.0/components/tooltips/)

Require

- `data-toggle="tooltip"` 
- `data-placement="top"` 
- `title="Tooltip on top"`
- `script`

option

- `data-html="true"`

<hr>

有加上 `data-html="true"` 後

就可以使用 `html標籤` --- `title="<em>按下 Enter 快速搜尋</em>"`

```html
	<div class="input-group">
            <input
              type="text"
              class="form-control form-control-sm"
              placeholder="Search for..."
              data-toggle="tooltip"
              data-placement="top"
              data-html="true"
              title="<em>按下 Enter 快速搜尋</em>"
            />
            <span class="input-group-btn">
              <button class="btn btn-secondary btn-sm" type="button">
                Go!
              </button>
            </span>
          </div>
```

```javascript
<script>
      $(document).ready(function() {
      
        $('[data-toggle="tooltip"]').tooltip()

      });
</script>
```

<br>

## 增加列表互動性

[Hoverable rows](https://getbootstrap.com/docs/4.0/content/tables/#hoverable-rows)

明顯讓使用者知道滑鼠現在在哪一列上面

<br>

[Contextual classes](https://getbootstrap.com/docs/4.0/content/tables/#contextual-classes)

可標示
 
- `出貨` `danger`
- `未出貨` `warning`

普遍性的 `已出貨` 就不用有色彩

這樣才不會讓畫面混亂

> 都是重點時 = 沒有重點

<br>

### progress

[Animated stripes](https://getbootstrap.com/docs/4.0/components/progress/#animated-stripes)

當頁面有很多 `Ajax` 在資料串接讀取時

可以增加一個 **Loading** 使用 `progress bar`

因為加上 `progress-bar-animated` 會比較吃 ***CPU*** 效能

不要讓他常駐的出現 , 必要時出現就好 .

<br>

## 動態操作

[Button group](https://getbootstrap.com/docs/4.0/components/button-group/)

將按鈕視為一個群組 , 會省去按鈕與按鈕之間的空間 .

細項的按鈕使用 `outline` 讓視覺感沒那麼重

<br>

[Split button dropdowns](https://getbootstrap.com/docs/4.0/components/dropdowns/#split-button-dropdowns)

將 ***不常用到*** 或 ***刪除訂單*** 放到下拉式選單


