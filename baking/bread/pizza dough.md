- [ ] activate yeast
	- [ ] 320g warm water
	- [ ] 13g granulated sugar
	- [ ] packet of instant yeast
	- [ ] cover and let rest for ~5 minutes
- [ ] add ingredients
	- [ ] 30g olive oil
	- [ ] 1 tsp salt
	- [ ] 440g+ all-purpose flour
- [ ] knead for 5 minutes
- [ ] let rise for 60-90 minutes
- [ ] bake
	- [ ] lay out and add toppings
	- [ ] 13-15 minutes @ 475°f
## ingredients
tags: #granulated_sugar, #instant_yeast, #olive_oil, #salt, #ap_flour
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
