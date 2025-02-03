# Leads
```dataview
table without id
	file.link as Name,
	last-contact as "Last Contact"
from #lead and -"Templates"
```

```dataviewjs
const {fieldmodifier: f}=
this.app.plugins.plugins["metadata-menu"].api;

dv.table
dv.pages('')
	.where(p => p.fileClass == 'Lead')
```