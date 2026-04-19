- [ ] wet mix
	- [ ] 3/4 cup melted butter
	- [ ] 150g brown sugar
	- [ ] 100g granulated sugar
	- [ ] 1 large egg
	- [ ] 1 egg yolk
	- [ ] 2 tsp vanilla extract
- [ ] dry mix
	- [ ] 280g all-purpose flour
	- [ ] 1 tsp baking soda
	- [ ] 1.5 tsp cornstarch
	- [ ] 1/2 tsp salt
- [ ] bake
	- [ ] add chocolate chips
	- [ ] 10-15 minutes @ 325°F
## ingredients
tags: #butter, #brown_sugar, #granulated_sugar, #egg, #vanilla_extract, #ap_flour, #baking_soda, #cornstarch, #salt, #chocolate
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
