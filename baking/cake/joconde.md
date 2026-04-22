- [ ] meringue (stiff peaks)
	- [ ] 3 egg whites
	- [ ] 20g granulated sugar
- [ ] dry mix
	- [ ] 150g almond flour
	- [ ] 150g powdered sugar
	- [ ] 40g ap flour
	- [ ] 3 eggs
- [ ] combine
	- [ ] fold 1/3 of meringue into dry mix
	- [ ] fold in remaining meringue
	- [ ] fold in 1/8 cup melted butter
- [ ] bake
	- [ ] lined half sheet (5mm thick)
	- [ ] 8-10 minutes @ 400°F
## ingredients
tags: #egg, #granulated_sugar, #almond_flour, #powdered_sugar, #ap_flour, #butter
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
