# Color

> [!NOTE]
> Markdown (.md) ফাইল-এ টেক্সট কালার দেওয়ার জন্য সরাসরি কোনো স্ট্যান্ডার্ড সিনট্যাক্স নেই, তবে কিছু কাজার উপায় আছে:


## 1. HTML ট্যাগ ব্যবহার করে (সবচেয়ে কম্প্যাটিবল সমাধান)
```bash
<span style="color:red">লাল টেক্সট</span>
```
Example: 
<span style="color:red">লাল টেক্সট</span>



## 2. CSS ক্লাস সহ HTML (GitHub/GitLab এ কাজ করবে না)
```bash
<style>
.blue-text { color: blue; }
</style>

<p class="blue-text">নীল টেক্সট</p>
```
Example: 
<style>
.blue-text { color: blue; }
</style>

<p class="blue-text">নীল টেক্সট</p>



## 3. ইনলাইন CSS (কিছু Markdown রেন্ডারার সাপোর্ট করে)
```bash
**<span style="color:#ff00ff">গোলাপি টেক্সট</span>**
```
**<span style="color:#ff00ff">গোলাপি টেক্সট</span>**




## 4. Markdown এক্সটেনশন ব্যবহার (Typora/Jupyter মতো টুলসে)
```bash
$\color{green}{সবুজ\ টেক্সট}$ 
```
Example: 
$\color{green}{সবুজ\ টেক্সট}$ 



## 1. HTML ট্যাগ ব্যবহার করে (সবচেয়ে কম্প্যাটিবল সমাধান)
```bash
```
Example: 




## 1. HTML ট্যাগ ব্যবহার করে (সবচেয়ে কম্প্যাটিবল সমাধান)
```bash
```
Example: 