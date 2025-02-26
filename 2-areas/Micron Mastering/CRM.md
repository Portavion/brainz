# Leads
```dataviewjs
const {fieldModifier: f}=
this.app.plugins.plugins["metadata-menu"].api;

dv.table(['Name','Url', 'Type', 'Initial DM', 'Engaged', 'Qualified', 'Lost', 'Last Contact', 'Date Added'],
dv.pages('')
	.where(p => p.fileClass == 'leads')
	.filter(p => !p.file.path.includes('classes'))
	.filter(p => !p.qualified || p.qualified==="Qualified" || p.qualified==="TBC")
	//.sort(p => p.Date, 'desc')
	.sort(p => p.file.name, 'asc')
	.map( p => [
		  p.file.link,
	      f(dv, p, 'Url'),
		  f(dv, p, 'Lead Type'),
		  f(dv, p, 'Initial DM'),
		  f(dv, p, 'Engaged'),
		  f(dv, p, 'Qualified'),
		  f(dv, p, 'Lost'),
		  f(dv, p, 'Last Contact'),
		  f(dv, p, 'Date')	  
	])
)
```
# Initial DM - Not Engaged Leads
```dataviewjs
const { fieldModifier: f } = this.app.plugins.plugins["metadata-menu"].api;

dv.table(
  ["Name", "Url", "Type", "Initial DM", "Engaged", "Qualified", "Lost", "Call Booked", "Last Contact"],
  dv.pages("")
    .where(
      (p) =>
        p.fileClass == "leads" &&
        !p.file.path.includes("classes") &&
        p["Initial DM"] && // Check if 'Initial DM' exists and is not empty
        !p["Engaged"] // Check if 'Engaged' is empty or null
    )
    .map((p) => [
      p.file.link,
      f(dv, p, "Url"),
      f(dv, p, "Lead Type"),
      f(dv, p, "Initial DM"),
      f(dv, p, "Engaged"),
      f(dv, p, "Qualified"),
      f(dv, p, "Lost"),
      f(dv, p, "Call Booked"),
      f(dv, p, "Last Contact"),
    ])
);
```
# All Leads - oldest contact first
const { fieldModifier: f } = this.app.plugins.plugins["metadata-menu"].api;

dv.table(
  ["Name", "Url", "Type", "Initial DM", "Engaged", "Qualified", "Lost", "Call Booked", "Last Contact"],
  dv.pages("")
    .where((p) => p.fileClass == "leads" && !p.file.path.includes("classes"))
    .sort(p => p["Last Contact"], 'asc') // Sorts by 'Last Contact' in ascending order (oldest first)
    .map((p) => [
      p.file.link,
      f(dv, p, "Url"),
      f(dv, p, "Lead Type"),
      f(dv, p, "Initial DM"),
      f(dv, p, "Engaged"),
      f(dv, p, "Qualified"),
      f(dv, p, "Lost"),
      f(dv, p, "Call Booked"),
      f(dv, p, "Last Contact"),
    ])
);
# Test
# Test
# Test
# Test

# All Leads
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