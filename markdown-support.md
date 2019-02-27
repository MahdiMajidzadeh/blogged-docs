# Markdown Support

Blogged automatically leverages Markdown to HTML parser out of the box.

---

- [Basics](#basics)
- [Tables](#tables)
- [Alarms](#alarms)

<a name="basics">
## Basics

Markdown elements automatically parsed into normal HTML tags.

<larecipe-badge type="success">Typography</larecipe-badge>

Input:

```text
###### H6
```

Output:

###### H6


<br>

<larecipe-badge type="success">Images</larecipe-badge>

Input:

```text
![image](url)
```

Output:

![cute image](https://media.tenor.com/images/f45c43d124468dc602a95baabadab70d/tenor.gif)

<br/>
<larecipe-badge type="success">Inline Code</larecipe-badge>

Input:

```text
Inline code is `cool`
```

Output:

Inline code is `cool`

<br/>
<larecipe-badge type="success">Code</larecipe-badge>

Blogged uses `prism.js` with code highlighting out of the box. Blogged supports all Prism supported languages.

Input:

\```php 
<br>
echo 'Blogged is beautiful';
<br>
\```

Output:

```php
echo 'Blogged is beautiful';
```


<a name="tables">
## Tables

Markdown Tables automatically parsed and converted to nice looking rendered tables. Thanks to Argon and CSS :D

Input: 

```markdown
| # | Name   | Age |
| : |   :-   |  :  |
| 1 | Saleem | 24  |
| 2 | John   | 25  |
| 3 | Ayman  | 26  |
```

Output: 

| # | Name   | Age |
| : |   :-   |  :  |
| 1 | Saleem | 24  |
| 2 | John   | 25  |
| 3 | Ayman  | 26  |

<a name="alarms">
## Alarms

Blogged provides beautiful looking alerts parsed directly from Markdown with extra sugar, all that you have to do is to prepend Markdown blockquote with `{type}` of your alert.

The supported alarms types are: **primary**, **success**, **info**, **danger**, **warning**.

Input: 

```text
> {danger} Here is an example of danger alarm message
```

Output:

> {danger} Here is an example of danger colored alarm
