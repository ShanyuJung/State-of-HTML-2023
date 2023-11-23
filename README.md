
## `State of HTML 2023`


[![State of HTML 2023](https://hackmd.io/_uploads/S1B55g5Np.png)](https://survey.devographics.com/zh-Hant/survey/state-of-html/2023)



<br/>


 ## `<datalist>`
比較像 dropdown 的 select element ?

還有附帶搜尋功能選項的功能

<br />


 ```jsx
    <input name="country" list="countries">
        <datalist id="countries">
        <option>Afghanistan</option>
          ...
    </datalist>
 ```
 
 
 <br/>
 
 
 [`<datalist>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/datalist) vs [`<select>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/select)


<br/>


## `<selectlist>`

真正的原生 dropdown element 來了

**現在還沒有任何一個瀏覽器可以用**


[Demo](https://open-ui.org/components/selectlist/)


<br/>

 
 ## `HTML Media Capture`
開啟手機前後鏡頭的 api

 
 <br/>
 
 
 
 ```jsx
     <input type="file" accept="video/*" capture="user">
```


<br/>


| Value | Description | 
| -------- | -------- | 
| user    | The user-facing camera and/or microphone should be used.    | 
| environment     | The outward-facing camera and/or microphone should be used     | 


<br/>

只支援手機，測過 macbook 不會觸發(用我自己的手機實測都是同一個鏡頭)

![Capture 支援度](https://hackmd.io/_uploads/By283eq4p.png)


<br/>


[MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/capture)


<br/>
<br/>


## `input.showPicker()`

操作各種類型的 input

<br/>



```jsx
    <input id="dateInput" type="date">
    <button onclick="dateInput.showPicker()">Select date</button>
```


<br/>


[MDN](https://developer.mozilla.org/en-US/docs/Web/API/HTMLInputElement/showPicker)

<br/>


## `FormData API`


- Content-Type: application/json 代表請求內容是 JSON
- Content-Type: image/png 代表請求內容是圖片檔


一般的 Content-Type 往往只能傳送一種形式的資料，但在網頁的應用當中我們還可能想要上傳檔案、圖片、影片在表單裡頭，這樣的需求促成了 multipart/form-data 規範的出現

最簡單發送一個 Content-Type 是 multipart/form data 的 request 就是透過 <form />


<br/>


```jsx=
    <form enctype="multipart/form-data" action="/upload" method="POST">
      <input type="text" name="name" />
      <input type="file" name="file" />
      <button>Submit</button>
    </form> 
```


<br/>


或是可以透過 FormData API

```javascript
    let fd = new FormData(form);
    let data = JSON.stringify(Object.fromEntries(fd));
```


<br/>


#### Reference
[一起理解 HTML 當中的 Form Data](https://blog.kalan.dev/2021-03-13-html-form-data)


<br/>




## `contenteditable="plaintext-only"`

Permits editing of the element's raw text, but not rich text formatting.

```jsx=
    <h2 class="title" contenteditable="plaintext-only"></h2>
```


[MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/contenteditable)



## `<details> and <summary>`

```jsx=
    <details>
        <summary>Details</summary>
        Longer content
    </details>
```


<details>
    <summary>Details</summary>
    Longer content
</details>


透過 open 屬性可以讓預設是展開的， 可以透過 <!--註解--> 方式註解

```jsx=
    <details open name="sidebar_panel" id="main_info">
	    <summary>Main info</summary>
	    <!-- controls -->
    </details>
    <details name="sidebar_panel" id="style_settings">
	    <summary>Style</summary>
	    <!-- controls -->
    </details>
```



<details open name="sidebar_panel" id="main_info">
	<summary>Main info</summary>
	<!-- controls -->
    content
</details>
<details name="sidebar_panel" id="style_settings">
	<summary>Style</summary>
	<!-- controls -->
    content2
</details>


<br/>


## `Popover API`

原生的彈窗

```jsx=
    <button popovertarget="mypopover">Toggle the popover</button>
    <div id="mypopover" popover>Popover content</div>
```


從 devtool 可以看出來他不是想我們常用的 `create portal` 的方法，而是透過 `::backdrop` 去控制，popover 的內容也始終在 HTML tree


![截圖 2023-11-22 上午12.15.06](https://hackmd.io/_uploads/S1fnPL9Na.png)



[DEMO](https://codepen.io/web-dot-dev/pen/poxQPWP)


<br/>


## `inert attribute`

Attribute to make an element and its descendants non-interactive, and invisible to assistive technology.


```jsx=
    <div id=app inert class=loading>
      ...
    </div>
```


**目前 React 並不支援 inert**

[React DOM: Support boolean values for inert prop #24730](https://github.com/facebook/react/pull/24730)


## `srcset and sizes attributes`

Attributes that allow providing several source images with hints to help the browser pick the right one.


```jsx=
    <img srcset="elva-fairy-480w.jpg 480w,
                 elva-fairy-800w.jpg 800w"
         sizes="(max-width: 600px) 480px,
                800px"
         src="elva-fairy-800w.jpg"
         alt="Elva dressed as a fairy">
```


<br/>

## `Resource Hints`

透過 `rel='dnsprefetch'` 來進行 `DNS Prefetching`，實際上就是預先做 DNS 解析（domain name resolution），將人類可理解的 domain name，轉為 IP address。


```jsx
    // 現在在 http://a.com 的路徑下
    <link rel="dns-prefetch" href="http://b.img.com.tw" />
    <link rel="dns-prefetch" href="http://c.img.com.tw" />
```


適合的對象
- 電商網站的商品頁大量載入不同 `domain` 下的商品圖，例如：淘寶
- 手機網頁，需要提高頁面載入完成的速度


[DNS Prefetching：預先做 DNS 解析，幫助網頁載入速度更快](https://www.cythilya.tw/2016/06/25/dns-prefetching/)


<br/>


## `Content-Security Policy (CSP)`

CSP 全名為 Content Security Policy 內容安全策略，它是一種電腦安全標準、網頁安全機制，目的在於防禦 跨網站指令碼攻擊(Cross-Site Scripting, XSS)、資源數據盜取(Cross-Site Data Theft, XSD)和網頁樣式置換…等代碼注入攻擊

CSP可以完全限制外部連入的檔案和行內語法,這是預設全部阻擋的寫法(最安全):

```javascript
    content-security-policy: default-src 'none';
```

或是以白名單的形式允許信任的外部來源:

```javascript
    content-security-policy: default-src 'none'; script-src 'self' https://ajax.googleapis.com;
```

[Content Security Policy (CSP) 筆記](https://hackmd.io/@Eotones/BkOX6u5kX)


<br/>


## `noreferrer noopener`


noopener 可以阻擋新開的網站使用 `window.opener` 而 `window.opener` 可以將原始網站跳轉至其他網頁，也可以取得原始網站的內容

referrer 指的是在送出請求時 headers 上的 Referer。使用 noreferrer 的話，在新網站上發送的 HTTP 請求的標頭不會帶上 Referer。此屬性值對於原本的網站沒有影響，但會影響新網站的流量分析和 SEO。在網站追蹤工具上會使用 referer 這個欄位來判斷來源網站，如果設定 noreferrer，該次造訪就會被視為直接流量(direct)，而非引薦(referral)。

```jsx=
<a href="https://www.gsscloud.com/tw/vital/bizform"
   target="_blank"
   rel="noreferrer" >
```


<br/>


## `blocking="render"`

Block rendering on a critical web font to prevent layout shifting or a flash of invisible/unstyled text. It also works in the preloading of critical resources of other types, like images, json, etc.

```jsx=
    <script blocking="render" async src="async-script.js"></script>
```


<br/>


## `<model> for AR/VR/3D content`

Allows embedding 3D graphical content into HTML.


```jsx=
    <model src="3d-assets/car"></model>
```



[github](https://github.com/immersive-web/model-element/blob/main/explainer.md)


<br/>


## `subgrid`

grid 新屬性，難用的 `<table />` 的替代品？



[MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_grid_layout/Subgrid)



[DEMO](https://codepen.io/wasfzuig/full/BavVgjm)



[Easy and more consistent layouts using subgrid](https://www.youtube.com/watch?v=IIQa9f0REtM)
