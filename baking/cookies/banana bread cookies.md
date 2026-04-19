- [ ] wet mix
	- [ ] 1/2 cup cubed butter
	- [ ] 150g brown sugar
	- [ ] 50g granulated sugar
	- [ ] 1 large egg
	- [ ] 1 overripe banana
	- [ ] 1 tsp vanilla extract
- [ ] dry mix
	- [ ] 340g ap flour
	- [ ] 1 tsp cornstarch
	- [ ] 1/2 tsp baking soda
	- [ ] 1/2 tsp salt
	- [ ] 1 tsp cinnamon
- [ ] bake
	- [ ] double scoop
	- [ ] 12-15 minutes @ 350°F
## ingredients
tags: #butter, #brown_sugar, #granulated_sugar, #egg, #banana, #vanilla_extract, #ap_flour, #cornstarch, #baking_soda, #salt, #cinnamon
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
