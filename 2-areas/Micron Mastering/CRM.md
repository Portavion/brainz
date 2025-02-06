# Leads
```dataviewjs
const {fieldModifier: f}=
this.app.plugins.plugins["metadata-menu"].api;

dv.table(['Name','Url', 'Type', 'Initial DM', 'Engaged', 'Qualified', 'Lost', 'Call Booked', 'Last Contact'],
dv.pages('')
	.where(p => p.fileClass == 'leads')
	.filter(p => !p.file.path.includes('classes'))
	.filter(p => !p.qualified || p.qualified==="Qualified" || p.qualified==="TBC")
	.map( p => [
		  p.file.link,
	      f(dv, p, 'Url'),
		  f(dv, p, 'Lead Type'),
		  f(dv, p, 'Initial DM'),
		  f(dv, p, 'Engaged'),
		  f(dv, p, 'Qualified'),
		  f(dv, p, 'Lost'),
		  f(dv, p, 'Call Booked'),
		  f(dv, p, 'Last Contact')
	])
)
```
# All leads
```dataviewjs
const {fieldModifier: f}=
this.app.plugins.plugins["metadata-menu"].api;

dv.table(['Name','Url', 'Type', 'Initial DM', 'Engaged', 'Qualified', 'Lost', 'Call Booked', 'Last Contact'],
dv.pages('')
	.where(p => p.fileClass == 'leads')
	.filter(p => !p.file.path.includes('classes'))
	.map( p => [
		  p.file.link,
	      f(dv, p, 'Url'),
		  f(dv, p, 'Lead Type'),
		  f(dv, p, 'Initial DM'),
		  f(dv, p, 'Engaged'),
		  f(dv, p, 'Qualified'),
		  f(dv, p, 'Lost'),
		  f(dv, p, 'Call Booked'),
		  f(dv, p, 'Last Contact')
	])
)
```