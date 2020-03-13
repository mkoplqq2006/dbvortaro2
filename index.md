## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/mkoplqq2006/dbvortaro.github.io/edit/master/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
import pymysql.cursors

conn = pymysql.connect(host='127.0.0.1',
                    user='root',
                    password='',
                    db='mysql',
                    charset='utf8mb4',
                    cursorclass=pymysql.cursors.DictCursor)
cursor = conn.cursor()
cursor.execute("select table_name from information_schema.tables where table_schema='mysql' and table_type='base table'")
tables = cursor.fetchall()

markdown_table_header = """### %s 
字段名 | 字段类型 | 默认值 | 注解
---- | ---- | ---- | ---- 
"""
markdown_table_row = """%s | %s | %s | %s
"""

f = open("mysql.md", "w", encoding="utf-8")
for table in tables:
    sql = 'select COLUMN_NAME,COLUMN_TYPE,COLUMN_DEFAULT,COLUMN_COMMENT from information_schema.COLUMNS where table_schema="mysql" and table_name="'+table['table_name']+'"'
    cursor.execute(sql)
    tmp_table = cursor.fetchall()
    p = markdown_table_header % table['table_name'];
    for col in tmp_table:
        p += markdown_table_row %(col['COLUMN_NAME'],col['COLUMN_TYPE'],col['COLUMN_DEFAULT'],col['COLUMN_COMMENT'])
    f.writelines(p)
f.close()
```

### db.py
```markdown
import pandas as pd
from tqdm import tqdm
import os

currentPath = os.path.dirname(os.path.abspath(__file__))
pd_frame = pd.read_excel(currentPath+'/xxxx.xlsx')

for i in tqdm(range(len(pd_frame))):
    B = pd_frame.iloc[i]["BB"]
    C = pd_frame.iloc[i]["CC"]
    D = pd_frame.iloc[i]["DD"]

    # print(B)
    # print(C)

    if (C !=""):
        f = open(B+".txt", "w", encoding="utf-8")
        f.writelines(C)
        f.close()

        f2 = open(B+"2.txt", "w", encoding="utf-8")
        f2.writelines(D)
        f2.close()
```
### diff.py
```markdown
import pandas as pd
import difflib
import time
import os
from tqdm import tqdm

currentPath = os.path.dirname(os.path.abspath(__file__))
pd_frame = pd.read_excel(currentPath+'/xxx.xlsx')

d = difflib.Differ()
d2 = difflib.HtmlDiff()

for i in tqdm(range(len(pd_frame))):
    B = pd_frame.iloc[i]["BB"]
    # print(B)

    f = open(currentPath+"\\"+B+".txt", "r", encoding="utf-8")
    # print(f.readlines())
    f2 = open(currentPath+"\\"+B+"2.txt", "r", encoding="utf-8")
    
    text1 = f.readlines()
    text2 = f2.readlines()

    diff = list(d.compare(text1, text2))
    for line in diff:
    	# print(line[0:1])
    	L = line[0:1]
    	if ("+"==L or "-"==L):
		    htmlContent = d2.make_file(text1, text2)
		    with open(B+".html", "w", encoding="utf-8") as f3:
		    	f3.write(htmlContent)
		    break

    f.close()
    f2.close()


```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/mkoplqq2006/dbvortaro.github.io/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.

<script async src="//busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js"></script>
<span id="busuanzi_container_site_pv">本站总访问量<span id="busuanzi_value_site_pv"></span>次</span>
