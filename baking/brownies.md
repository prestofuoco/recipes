- [ ] wet mix
	- [ ] 3/4 cup butter
	- [ ] 400g granulated sugar
	- [ ] 3 large eggs
	- [ ] 2 tsp vanilla extract
- [ ] dry mix
	- [ ] 125g all-purpose flour
	- [ ] 82g cocoa powder
	- [ ] 1 tsp salt
- [ ] bake
	- [ ] 200g+ coarsely chopped chocolate
	- [ ] 30-32 minutes @ 350°F
## ingredients
tags: #butter, #granulated_sugar, #egg, #vanilla_extract, #ap_flour, #cocoa_powder, #salt, #chocolate
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
