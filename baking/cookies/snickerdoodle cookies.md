- [ ] wet mix
	- [ ] 1 cup butter
	- [ ] 270g granulated sugar
	- [ ] 1 large egg
	- [ ] 1 egg yolk
	- [ ] 2 tsp vanilla extract
- [ ] dry mix
	- [ ] 380g all-purpose flour
	- [ ] 2 tsp cream of tartar
	- [ ] 1 tsp baking soda
	- [ ] 1.5 tsp ground cinnamon
	- [ ] 0.5 tsp salt
- [ ] topping
	- [ ] 70g granulated sugar
	- [ ] 1 tsp ground cinnamon
- [ ] bake
	- [ ] roll cookie dough balls in topping mixture
	- [ ] 10-12 minutes @ 375°F
## ingredients
tags: #butter, #granulated_sugar, #egg, #vanilla_extract, #ap_flour, #cream_of_tartar, #baking_soda, #cinnamon, #salt
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
