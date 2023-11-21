![State of HTML 2023](https://hackmd.io/_uploads/S1B55g5Np.png)


 ## <datalist />
 
 ### 比較像 dropdown 的 select element
 ```jsx
    <input name="country" list="countries">
        <datalist id="countries">
        <option>Afghanistan</option>
          ...
    </datalist>
 ```
 [<datalist />](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/datalist) vs [<select />](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/select)
 
 
 ## HTML Media Capture
 
 開啟手機前後鏡頭的 api
 
 ```jsx
     <input type="file" accept="video/*" capture="user">
````


| Value | Description | 
| -------- | -------- | 
| user    | The user-facing camera and/or microphone should be used.    | 
| environment     | The outward-facing camera and/or microphone should be used     | 

只支援手機，測過 macbook 不會觸發(用我自己的手機實測都是同一個鏡頭)

![Capture 支援度](https://hackmd.io/_uploads/By283eq4p.png)
[MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/capture)