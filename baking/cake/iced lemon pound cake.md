- [ ] wet mix
  - [ ] 1 cup butter
  - [ ] 200g granulated sugar
  - [ ] 3 eggs
  - [ ] 60g greek yogurt
  - [ ] 45g lemon juice
  - [ ] 1 tsp lemon zest
  - [ ] 1 tsp vanilla extract
- [ ] dry mix
  - [ ] 188g all-purpose flour
  - [ ] 1.5 tsp baking powder
  - [ ] 0.5 tsp salt
- [ ] bake
  - [ ] 9 inch loaf pan
  - [ ] 55-65 minutes @ 350°F
## ingredients
tags: #butter, #granulated_sugar, #egg, #greek_yogurt, #lemon, #vanilla_extract, #ap_flour, #baking_powder, #salt
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
