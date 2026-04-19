- [ ] wet mix
    - [ ] 3/2 cup unsalted butter
    - [ ] 400g granulated sugar
    - [ ] 3 large eggs
    - [ ] 2 egg whites
    - [ ] 1 tbsp vanilla extract
- [ ] dry mix
    - [ ] 433g cake flour
    - [ ] 1 tsp salt
    - [ ] 2 tsp baking powder
    - [ ] 3/4 tsp baking soda
- [ ] combine
    - [ ] mix in 360g buttermilk just until combined
- [ ] bake
    - [ ] three 9 inch cake pans
    - [ ] 23-26 minutes @ 350°F
## ingredients
tags: #butter, #granulated_sugar, #egg, #vanilla_extract, #cake_flour, #salt, #baking_powder, #baking_soda
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
