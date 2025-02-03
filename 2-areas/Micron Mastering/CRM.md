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

dv.table(['Name', 'Type', 'Initial DM', 'Engaged', 'Qualified', 'Lost', 'Call Booked'])
dv.pages('')
	.where(p => p.fileClass == 'Lead')
	.filter(p => !p.file.path.includes('classes'))
	.map( p => p.file.link,
		  f(dv, p, 'Lead Type'),
		  f(dv, p, 'Initial DM',
		  f(dv, p, 'Engaged'),
		  f(dv, p, 'Qualified'),
		  f(dv, p, 'Lost'),
		  f(dv, p, 'Call Booked')))
```