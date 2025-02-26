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
# All Contacted Leads - Newest first
```dataviewjs
const { fieldModifier: f } = this.app.plugins.plugins["metadata-menu"].api;

dv.table(
  ["Name", "Url", "Type", "Initial DM", "Engaged", "Qualified", "Lost", "Call Booked", "Last Contact"],
  dv.pages("")
    .where(
      (p) =>
        p.fileClass == "leads" &&
        !p.file.path.includes("classes") &&
        p["Initial DM"] &&
        p["Last Contact"]
    )
    .sort((p) => p["Last Contact"], "desc")
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
# All Contacted Leads - Oldest contacted first
```dataviewjs
const { fieldModifier: f } = this.app.plugins.plugins["metadata-menu"].api;

dv.table(
  ["Name", "Url", "Type", "Initial DM", "Engaged", "Qualified", "Lost", "Call Booked", "Last Contact"],
  dv.pages("")
    .where(
      (p) =>
        p.fileClass == "leads" &&
        !p.file.path.includes("classes") &&
        p["Initial DM"] &&
        p["Last Contact"]
    )
    .sort((p) => p["Last Contact"], "asc")
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
# Test
```dataviewjs
const { fieldModifier: f } = this.app.plugins.plugins["metadata-menu"].api;

dv.table(
  ["Name", "Url", "Type", "Lost Date", "Last Contact"],
  dv.pages("")
    .where(
      (p) =>
        p.fileClass == "leads" &&
        !p.file.path.includes("classes") &&
        p["Lost"] // Assuming you have a 'Lost' field to mark lost leads
    )
    .sort((p) => p["Lost Date"], "desc") // Sort by 'Lost Date' in descending order (newest first)
    .map((p) => [
      p.file.link,
      f(dv, p, "Url"),
      f(dv, p, "Lead Type"),
      f(dv, p, "Lost Date"),
      f(dv, p, "Last Contact"),
    ])
);
```
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