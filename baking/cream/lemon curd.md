- [ ] mix in saucepan
	- [ ] 90g granulated sugar
	- [ ] 4 egg yolks
	- [ ] 80g lemon juice
	- [ ] 8g lemon zest
	- [ ] 2g salt
- [ ] saucepan on medium-low
	- [ ] stir until just thickened
	- [ ] remove from heat
- [ ] mix in
	- [ ] 1/4 cup cubed butter
## ingredients
tags: #granulated_sugar #egg #lemon #salt #butter
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