- [ ] wet mix
	- [ ] 1/2 cup butter
	- [ ] 150g granulated sugar
	- [ ] 2 large eggs
	- [ ] 2 tsp vanilla extract
	- [ ] 120g greek yogurt
	- [ ] 2 tbsp milk
- [ ] dry mix
	- [ ] 166g all-purpose flour
	- [ ] 1 tsp baking powder
	- [ ] 1/4 tsp baking soda
	- [ ] 1/4 tsp salt
- [ ] cinnamon crumb mixture
	- [ ] 135g brown sugar
	- [ ] 95g all-purpose flour
	- [ ] 2.5 tsp ground cinnamon
	- [ ] 6 tbsp butter, cold and cubed
- [ ] vanilla icing
	- [ ] 120g powdered sugar, sifted
	- [ ] 1/2 tsp vanilla extract
	- [ ] 2 tbsp heavy cream
- [ ] bake
	- [ ] 8-inch square pan
	- [ ] batter, crumb mixture, batter, crumb mixture
	- [ ] 35-40 minutes @ 350°F
## ingredients
tags: #butter, #granulated_sugar, #egg, #vanilla_extract, #greek_yogurt, #milk, #ap_flour, #baking_powder, #baking_soda, #salt, #brown_sugar, #cinnamon, #powdered_sugar, #heavy_cream
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
