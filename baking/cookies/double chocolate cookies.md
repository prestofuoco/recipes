- [ ] wet mix
	- [ ] 1/2 cup butter
	- [ ] 100g granulated sugar
	- [ ] 110g brown sugar
	- [ ] 1 large egg
	- [ ] 1 tsp vanilla extract
- [ ] dry mix
	- [ ] 125g all-purpose flour
	- [ ] 55g cocoa powder
	- [ ] 1 tsp baking soda
	- [ ] 1/8 tsp salt
	- [ ] 1 tbsp milk
- [ ] bake
	- [ ] 225g chocolate chips
	- [ ] 10-12 minutes @ 350°F
## ingredients
tags: #butter, #granulated_sugar, #brown_sugar, #egg, #vanilla_extract, #ap_flour, #cocoa_powder, #baking_soda, #salt, #milk, #chocolate
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
