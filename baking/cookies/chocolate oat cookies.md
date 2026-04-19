- [ ] wet mix
	- [ ] 1/2 cup butter, browned
	- [ ] 100g brown sugar
	- [ ] 50g granulated sugar
	- [ ] 1 egg
	- [ ] 1 tsp vanilla extract
- [ ] dry mix
	- [ ] 130g ap flour
	- [ ] 90g rolled oats
	- [ ] 1 tsp baking soda
	- [ ] 1 tsp cinnamon 
	- [ ] 1 tsp coarse salt
	- [ ] dark chocolate
- [ ] bake
	- [ ] single scoop
	- [ ] 10-12 minutes @ 350°F
## ingredients
tags: #butter, #brown_sugar, #granulated_sugar, #egg, #vanilla_extract, #ap_flour, #baking_soda, #cinnamon, #salt, #chocolate
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
