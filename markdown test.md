# 標題

# 一級標題 (大標)  
## 二級標題 (中標)
### 三級標題 (小標)

- 無序清單項目 1
- 無序清單項目 2

1. 有序清單第一點
2. 有序清單第二點
---
# 字體
顏色	語法範例	呈現效果</br>
紅色	$\color{red}{\text{重點文字}}$	顯示紅色文字  
綠色	$\color{green}{\text{成功/完成}}$	顯示綠色文字</br>
藍色	$\color{blue}{\text{提示/連結}}$	顯示藍色文字</br>
橘色	$\color{orange}{\text{注意}}$	顯示橘色文字</br>

行內程式碼會在文字後方加上淡淡的灰色區塊。呈現： 重點內容</br>
語法： `文字內容` </br>

刪除線語法</br>
語法： ~~被刪除的文字~~ </br>
語法：<s>你要刪除的文字</s>

插入連結</br>
[點我前往 YouTube](https://www.youtube.com/)

把字串的前後標在四個等號中間 ==要標色的字== 就會有螢光筆的效果！</br>

---
# 程式碼
JAVA 範例
```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello!");
    }
}
```
多層引用
> 第一層引用
> > 第二層巢狀引用
> > > 第三層...
> > > >

---
# 收合
<details>
  <summary>點擊展開查看詳情</summary>

  這裡是隱藏的內容，可以包含：
  * 文字說明
  * [連結](https://github.com)
  * `程式碼`
</details>

### 在表格 (Table) 內使用收合
| 功能名稱 | 詳細說明 |
| :--- | :--- |
| 圖片預覽 | <details><summary>展開圖片</summary><img src="https://github.com/user-attachments/assets/3b21d08e-880d-474b-957d-c635db494078" width="300"></details> |
| 程式邏輯 | <details><summary>查看代碼</summary>這段邏輯處理了...<br>1. 驗證<br>2. 儲存</details> |
| 逆風高飛 |


### 在收合區塊內放「程式碼區塊」
這點最容易出錯！ 如果要在收合區塊內放入有語法高亮的程式碼區塊（使用 ` ` ` ），請務必在 < summary > 下方空一行，否則程式碼區塊會跑版。

<details>
  <summary>點擊查看 Python 範例</summary>

  ```python
  def hello_world():
      print("Hello GitHub!")
  ```
</details>

### 預設為「開啟」狀態，內容預設是展開的，使用者可以點擊收合，只需在標籤加上 `open`：

<details open>
  <summary>預設已展開的區塊</summary>
  內容在此...

</details>

---
# 圖片
GitHub 上，有幾種常見的方式可以存放並引用圖片：</br>
專案內路徑： 如果圖片在你的 Repository 裡，使用相對路徑： ![說明](./images/Lab.png)</br>
直接上傳： 在 GitHub 的 Issue 或 Pull Request 留言框中直接「拖放」圖片，會自動生成一個以 https://user-images.githubusercontent.com/... 開頭的連結，你可以複製這個連結貼到 .md 檔裡。</br>
外部連結： 直接使用任何圖床或網路上公開的圖片網址。</br>
也可以直接截圖後複製貼上</br>

---
# 表格
| 項目 | 縮圖 (HTML 控制) | 說明 |
| :--- | :--- | :--- |
| 螢幕截圖 | <img src="https://www.shutterstock.com/image-photo/adolf-hitler-giving-nazi-salute-260nw-242815222.jpg" width="300"> | 使用 HTML 控制寬度為 300px |

---
# 註解
<!-- 這是單行註解 -->
<!-- 這會被渲染成... \n 另一行 -->
