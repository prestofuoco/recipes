- [ ] wet mix
	- [ ] 3/4 cup unsalted butter
	- [ ] 350g granulated sugar
	- [ ] 5 large egg whites
	- [ ] 120g greek yogurt
	- [ ] 1 tbsp vanilla extract
	- [ ] 240g whole milk
- [ ] dry mix
	- [ ] 295g cake flour
	- [ ] 2 tsp baking powder
	- [ ] 0.5 tsp baking soda
	- [ ] 1 tsp salt
- [ ] bake
	- [ ] two 9 inch cake pans
	- [ ] 24-25 minutes @ 350°F
## ingredients
tags: #butter, #granulated_sugar, #egg, #greek_yogurt, #vanilla_extract, #milk, #cake_flour, #baking_powder, #baking_soda, #salt
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
