- [ ] wet mix
	- [ ] 3/4 cup butter
	- [ ] 225g granulated sugar
	- [ ] 1 egg
	- [ ] 1 tsp vanilla extract
	- [ ] 2 lemons
		- [ ] 60g lemon juice
		- [ ] 1 tbsp lemon zest
- [ ] dry mix
	- [ ] 310g ap flour
	- [ ] 1 tsp cornstarch
	- [ ] 1 tsp baking soda
	- [ ] 1/2 tsp salt
- [ ] rolling
	- [ ] 35g granulated sugar
	- [ ] 120g powdered sugar
- [ ] bake
	- [ ] chill for at least 3 hours
	- [ ] roll in sugar blend
	- [ ] 12-13 minutes @ 350°F
## ingredients
tags: #butter, #granulated_sugar, #egg, #vanilla_extract, #lemon, #ap_flour, #cornstarch, #baking_soda, #salt, #powdered_sugar
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
