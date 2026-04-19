- [ ] combine in saucepan
	- [ ] 125g water
	- [ ] 125g milk
	- [ ] 1/2 cup butter
	- [ ] 1/2 tsp salt
	- [ ] 1 tsp granulated sugar
	- [ ] cook to boil
	- [ ] 150g bread flour
	- [ ] mix in vigorously until thin film forms
- [ ] transfer to mixing bowl
	- [ ] beat for 3 minutes, until no steam
	- [ ] whisk 5 eggs in separate bowl
	- [ ] add in one at a time, stop when glossy
- [ ] bake
	- [ ] 400°F for 15 minutes
	- [ ] 350°F for 20 minutes
## ingredients
tags: #milk, #butter, #salt, #granulated_sugar, #bread_flour
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
