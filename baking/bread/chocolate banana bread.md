- [ ] wet mix
	- [ ] 2 beaten eggs
	- [ ] 1/2 cup butter
	- [ ] 135g granulated sugar
	- [ ] 1/2 tsp vanilla extract
	- [ ] 3 overripe bananas
- [ ] dry mix
	- [ ] 120g all-purpose flour
	- [ ] 28g cocoa powder
	- [ ] 1 tsp baking soda
	- [ ] 1/2 tsp salt
- [ ] add in
	- [ ] ~170g chocolate chips
- [ ] bake
	- [ ] 9 inch loaf pan
	- [ ] 50-60 minutes @ 350°F
## ingredients
tags: #butter, #granulated_sugar, #vanilla_extract, #banana, #ap_flour, #cocoa_powder, #baking_soda, #salt, #chocolate
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
