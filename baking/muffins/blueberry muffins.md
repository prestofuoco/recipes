- [ ] topping
	- [ ] 100g brown sugar
	- [ ] 67g chopped walnuts
	- [ ] 1 tsp ground cinnamon
- [ ] wet mix
	- [ ] 113g unsalted butter
	- [ ] 100g granulated sugar
	- [ ] 50g brown sugar
	- [ ] 2 eggs
	- [ ] 120g greek yogurt
	- [ ] 2 tsp vanilla extract
	- [ ] 60g milk
- [ ] dry mix
	- [ ] 220g all-purpose flour
	- [ ] 1 tsp baking powder
	- [ ] 1 tsp baking soda
	- [ ] 1/2 tsp salt
- [ ] bake
	- [ ] 210g blueberries
	- [ ] 12-count muffin pan
	- [ ] press topping mixture onto surface
	- [ ] 5 minutes @ 425°F
	- [ ] 18-20 minutes @ 350°F
## ingredients
tags: #brown_sugar, #walnut, #cinnamon, #butter, #granulated_sugar, #egg, #greek_yogurt, #vanilla_extract, #milk, #ap_flour, #baking_powder, #baking_soda, #salt, #blueberry
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
