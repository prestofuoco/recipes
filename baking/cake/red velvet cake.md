- [ ] wet mix
	- [ ] 1/2 cup unsalted butter
	- [ ] 400g granulated sugar
	- [ ] 240g vegetable oil
	- [ ] 4 egg yolks
	- [ ] 1 tbsp vanilla extract
	- [ ] 1 tsp white vinegar
	- [ ] 2 tsp red gel food coloring
- [ ] dry mix
	- [ ] 360g cake flour
	- [ ] 1 tsp baking soda
	- [ ] 10g cocoa powder
	- [ ] 1/2 tsp salt
- [ ] combine
	- [ ] slowly add dry ingredients alternating with 240g buttermilk
	- [ ] beat in food coloring
	- [ ] whip 4 egg whites until fluffy and fold into batter
- [ ] bake
	- [ ] two 9 inch cake pans
	- [ ] 30-32 minutes @ 350°F
## ingredients
tags: #butter, #granulated_sugar, #vegetable_oil, #egg, #vanilla_extract, #vinegar
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
