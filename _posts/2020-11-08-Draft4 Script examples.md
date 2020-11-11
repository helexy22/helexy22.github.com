---
layout:     post   				    # 使用的布局（不需要改）
title:     Drafts 4 keyboard 脚本分享				# 标题 
subtitle:   日常记录的超频脚本分享，包括插入时间，剪切等  #副标题
date:       2020-01-10 				# 时间
author:     helexy22 						# 作者
# header-img: img/post-bg-2015.jpg  #这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - Tool
    - iOS
---

官方网站：[Agile Tortoise](https://agiletortoise.zendesk.com/hc/en-us)

## Toolbar

<img src="https://raw.githubusercontent.com/helexy22/images/master/2020/Drafts%204%20keyBoard.jpg"/>

<center style="color:#C0C0C0;text-decoration:underline">Drafts 4 Toolbar</center>

## 常用的脚本

**1.自定义的时间戳**

```JavaScript
function getDateTime() {

    var now = new Date(); 
    var year = now.getFullYear();
    var month = now.getMonth()+1; 
    var day = now.getDate();
    var hour = now.getHours();
    var minute = now.getMinutes();
    var second = now.getSeconds(); 

    if(month.toString().length == 1) {
        var month = '0'+month;
    }
    if(day.toString().length == 1) {
        var day = '0'+day;
    } 
    if(hour.toString().length == 1) {
        var hour = '0'+hour;
    }
    if(minute.toString().length == 1) {
        var minute = '0'+minute;
    }
    if(second.toString().length == 1) {
        var second = '0'+second;
    } 

    var dateTime = year+'-'+month+'-'+day+' '+hour+':'+minute+':'+second; 
    return dateTime;

}

setSelectedText(getDateTime());

//移动光标到末尾
setSelectedRange(getText().length,0);

```

**2.剪切当前内容**

```javascript
var fullText=getText();

if fullText.toString().length != 0{
    setClipboard(fullText);
}

setText();
```



## Script Keys

- getText() : Returns the full text currently being edited.
- setText(string) : Replaces full text being edited with string.
- getSelectedText() : Return only the selected text. If no text selection exists, this will return an empty string.
- setSelectedText(string) : Replace only the current selected text range with the string. Also updates the selected range to match any change in length of the new string.
- getTextInRange(start, length) : Return text in the request range.
- setTextInRange(start, length, string) : Replace the text in the specified range with the value of string.
- getSelectedLineRange() : Returns the range (start,length) of the full line based on the current cursor position
- getSelectedRange() : Returns the current selected text range as an array with values [start, length].
- setSelectedRange(start, length) : Set the selected range of text. Invalid ranges will be automatically adjusted, and this text selection will be applied after successful completion of the script. 
- getClipboard(): Returns current contents of the system clipboard.
- setClipboard(string): Set the system clipboard to the string passed.
- markdown(string, useXHTML) : runs the string through the Markdown processor returning HTML.
- encodeHTMLEntities(string) : Encodes the string to HTML safe entities, e.g. converting & to &amp;
- decodeHTMLEntities(string) : Decodes HTML entities.

## Templates and Tags

- [[draft]] : The full text of the draft.
- [[title]] : The first line of the draft only.
- [[body]] : The remainder of the draft text after the first line is removed.
- [[selection]] : If text was selected within the draft before selecting an action, this tag will return only that selected text. If no text was selected, it will return the full text of the draft.
- [[line|n]] : The text of a specific line number in the draft, where “n” is the line number. i.e. [[line|1]], [[line|2]].
- [[line|n..n]] : In addition to specific lines, the lines tag (above) can accept ranges of lines, such as “[[line|2..5]]” for lines 2 through 5. This initial or trailing number in the range can be omitted to indicate the beginning or end, i.e. [[line|2..]] is line 2 through the end of the draft, [[line|..4]] is the first for lines of the draft.
- [[uuid]] : A unique identifier for the current draft.
- [[draft_open_url]] : A URL which can be used as a bookmark to open Drafts and select the current draft.
- [[clipboard]] : The current contents of the iOS clipboard.
- [[date]] : Timestamp in the format YYYY-MM-DD.
- [[date|format]] : Timestamp, formatted based on a custom strfime format string. For example [[date|%m-%d-%Y]] becomes “01–02–2013”. Read Dr. Drang’s great post on Drafts’ format strings for more ideas.
- [[created|format]] : Same as “date”, but returns the timestamp for the creation of the draft, rather than the current time.
- [[modified|format]] : Same as “date”, but returns the timestamp for the last modification date of the draft content, rather than the current time.
- [[longitude]] : The current device location longitude. **
- [[latitude]] : The current device location latitude. **
- [[created_longitude]] : The location longitude where the draft was created. **
- [[created_latitude ]] : The location latitude where the draft was created. **
- [[modified_longitude]] : The location longitude where the content of the draft was last modified. **
- [[modified_latitude]] : The location latitude where the content of the draft was last modified. **
- [[selection_start]] : The integer index of the start location of the last text selection in the draft.
- [[selection_length]] : The number of characters in the last text selection in the draft.
- [[time]] : Timestamp in the format YYYY-MM-DD-HH-MM-SS.
- {{ }} : Wrap text in double-curly brackets to have the text URL encoded.
%% %% : Wrap text in double percent signs to run the enclosed text through the Markdown engine and convert it to HTML.  This is useful to export Markdown to HTML, use in HTML Preview steps or other purposes.  By default, HTML5 compliant HTML is generated, but if you include the xhtml parameter, like %%xhtml|...%%, XHTML will be output.  This is needed to generate HTML compatible with Evernote's ENML markup.


## 资料

- [New flexible timestamps in Drafts - All this](http://www.leancrew.com/all-this/2013/02/new-flexible-timestamps-in-drafts/)
- [Script Keys – Agile Tortoise](https://agiletortoise.zendesk.com/hc/en-us/articles/202465564-Script-Keys)
- [Drafts Script Reference](https://scripting.getdrafts.com/)
- ⭐[Drafts Directory | Drafts Action Directory](https://actions.getdrafts.com/)

