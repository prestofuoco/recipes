- [ ] wet mix
	- [ ] 1/2 cup butter
	- [ ] 165g brown sugar
	- [ ] 2 large eggs
	- [ ] 3 overripe bananas
- [ ] dry mix
	- [ ] 250g all-purpose flour
	- [ ] 1 tsp baking soda
	- [ ] 1/2 tsp salt
- [ ] bake
	- [ ] 9 inch loaf pan
	- [ ] add chocolate chips
	- [ ] 60 minutes @ 350°F
## ingredients
tags: #butter, #brown_sugar, #egg, #banana, #ap_flour, #baking_soda, #salt
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
