- [ ] wet mix
	- [ ] 250g whole milk
	- [ ] 110g vegetable oil
	- [ ] 2 large eggs
	- [ ] 2 tsp vanilla extract
- [ ] dry mix
	- [ ] 250g all-purpose flour
	- [ ] 400g granulated sugar
	- [ ] 80g cocoa powder
- [ ] combine
	- [ ] mix on medium speed until combined
	- [ ] slowly add 230g boiling water
- [ ] bake
	- [ ] two 9 inch cake pans
	- [ ] 30-35 minutes @ 350°F
## ingredients
tags: #milk, #vegetable_oil, #egg, #vanilla_extract, #ap_flour, #granulated_sugar, #cocoa_powder
```dataviewjs
const groceries = dv.page("groceries");
if (!groceries) {
  dv.paragraph("missing: groceries.md not found");
} else {
  const recipeTags = (dv.current().file.etags ?? [])
    .map((t) => t.replace(/^#/, "").replace(/_/g, " "));
  const groceryTasks = (groceries.file.tasks ?? []).map((t) => ({
    name: String(t.text || "").trim().toLowerCase(),
    completed: Boolean(t.completed),
  }));
  const uniqueTags = [...new Set(recipeTags.map((t) => t.toLowerCase()))];
  const missing = uniqueTags.filter((tag) => {
    const item = groceryTasks.find((g) => g.name === tag);
    return !item || !item.completed;
  });
  if (missing.length === 0) {
    dv.paragraph("missing: none");
  } else {
    const missingTags = missing.map((m) => `#${m.replace(/ /g, "_")}`);
    dv.paragraph(`missing: ${missingTags.join(", ")}`);
  }
}
```
