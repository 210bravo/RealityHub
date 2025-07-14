## Seedling 

```datacorejsx
const { sortByDate } = await dc.require("Hidden/Datacore/Utilities/sort.js");
const COLUMNS = [  
{ id: "Name", value: page => page.$link },  
{ id: "Created", value: page => page.value("Created")
},
];  

return function View() {  
const pages = dc.useQuery('@page and !path("Hidden") and contains(Status, "🌱") OR contains(file.$tags, "🌱")');

const sortedPages = dc.useMemo(
() => pages.sort(sortByDate('Created', 'desc')), [pages])

return <dc.VanillaTable columns={COLUMNS} rows={pages} paging={10} />;  
}
```

## Fern 

## Tree