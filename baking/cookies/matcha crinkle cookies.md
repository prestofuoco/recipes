- [ ] wet mix
	- [ ] 1/2 cup butter
	- [ ] 200g granulated sugar
	- [ ] 2 eggs
- [ ] dry mix
	- [ ] 250g all-purpose flour
	- [ ] 30g matcha powder
	- [ ] 1 tsp baking powder
	- [ ] 1/2 tsp salt
	- [ ] 1/8 tsp baking soda
- [ ] rolling
	- [ ] 50g granulated sugar
	- [ ] 60g powdered sugar
- [ ] bake
	- [ ] 13-15 minutes @ 350°F
## ingredients
tags: #butter, #granulated_sugar, #egg, #ap_flour, #matcha_powder, #baking_powder, #salt, #baking_soda, #powdered_sugar
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
