- [ ] saucepan
	- [ ] 475g heavy cream
	- [ ] 1/8 tsp salt
	- [ ] cook over low heat until just hot
	- [ ] let sit for a few minutes
	- [ ] add 1 tsp vanilla extract
- [ ] wet mix
	- [ ] 5 egg yolks
	- [ ] 100g granulated sugar
- [ ] bake
	- [ ] slowly add vanilla cream mixture to egg mixture
	- [ ] pour into four ramekins
	- [ ] place in baking dish filled with boiling hot water, halfway up ramekins
	- [ ] 30-40 minutes @ 325°F, until centers are barely set
- [ ] let cool and refrigerate for several hours
## ingredients
tags: #heavy_cream, #salt, #egg, #granulated_sugar
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
