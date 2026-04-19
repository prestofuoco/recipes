- [ ] wet mix
	- [ ] 6 tbsp melted butter
	- [ ] 135g brown sugar
	- [ ] 1 egg
	- [ ] 1 tsp vanilla extract
	- [ ] 30g milk
	- [ ] 3 bananas
- [ ] dry mix
	- [ ] 190g ap flour
	- [ ] 1 tsp baking powder
	- [ ] 1 tsp baking soda
	- [ ] 1/2 tsp salt
	- [ ] 1 tsp ground cinnamon
	- [ ] 1/4 tsp ground nutmeg
- [ ] bake
	- [ ] add mix-ins
	- [ ] scoop into cupcake liners
	- [ ] 5 minutes @ 425°F
	- [ ] 16-18 minutes @ 350°F
## ingredients
tags: #butter, #brown_sugar, #egg, #vanilla_extract, #milk, #banana, #ap_flour, #baking_powder, #baking_soda, #salt, #cinnamon, #ground_nutmeg
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
