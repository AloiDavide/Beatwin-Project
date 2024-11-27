---
aliases: 
cssclasses:
  - red-links
  - blue-truth
  - blue-links
---


## Crime scene of the [[Chapel]]
- abc
- 1234
- _im[[por]]tant [[red link]]_. Not important [[normal link]].

> [!NOTE|c-plain bg-plain]+ # Crime scene of the [[Chapel]]
> - Contents
> - abc
> - _im[[por]]tant [[red link]]_. Not important [[normal link]].


`/>\s*\[\![^\n]*\n(?:>\s*.*\n)*/g`

```dataview
table
"!"+file.link
from #callout 
```

`="!"+[[Callout3]].file.link`

### Yo, this is definitely going somewhere
- [ ] Inlude if first line contains one of Mystery, Deduction, Hypothesis. Else ignore
- [ ] Group by type
	- [ ] Separate views?
- [ ] Improve views
	- [ ] grid if possible
	- [ ] maybe cards
- [ ] Add views to canvas


```dataviewjs
const pages = dv.pages('')

// This regex will find the contents of a specifically formatted callout
//const regex = />\s\[\!NOTE\]\s(.+?)((\n>\s.*?)*)\n/
const regex = />\s*\[\![^\n]*\n(?:>\s*[^\n]*\n)*/g


const rows = []
for (const page of pages) { 
	const file = app.vault.getAbstractFileByPath(page.file.path)
	// Read the file contents 
	const contents = await app.vault.read(file) 
	// Extract the summary via regex 
	for (const callout of contents.match(new RegExp(regex, 'sg')) || []) { 
		if(callout.split('\n')[0].contains("Deduction")){
			//rows.push([callout.split('\n')[0], callout, page.file.link]) 
		}
		rows.push([callout.split('\n')[0], callout, page.file.link]) 
	} 
}

dv.table(['Type', 'Callout', 'Note'], rows)
```




