- [ ] wet mix
	- [ ] 6 tbsp butter
	- [ ] 100g brown sugar
	- [ ] 65g granulated sugar
	- [ ] 2 large eggs
	- [ ] 125g sourdough starter
	- [ ] 3 overripe bananas
- [ ] dry mix
	- [ ] 190g all-purpose flour
	- [ ] 1 tsp baking soda
	- [ ] 1/2 tsp salt
- [ ] swirl
	- [ ] take 1/3 of batter and combine with hojicha paste
		- [ ] 10g hojicha
		- [ ] 15g hot water
	- [ ] pour 1/2 plain batter into 9x5 loaf pan
	- [ ] spoon dollops of hojicha batter
	- [ ] pour rest of plain batter on top
	- [ ] swirl with a butter knife, figure eight pattern
- [ ] bake
	- [ ] pour a line of melted butter along the center
	- [ ] 60-65 minutes @ 350°F
## ingredients
tags: #butter, #brown_sugar, #egg, #banana, #ap_flour, #baking_soda, #salt, #hojicha_powder
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