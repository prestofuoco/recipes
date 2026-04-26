- [ ] tangzhong
	- [ ] 30g ap flour
	- [ ] 150g milk
- [ ] dough
	- [ ] 90g milk
	- [ ] 90g warm water
	- [ ] instant yeast packet
	- [ ] 50g granulated sugar
	- [ ] 510g ap flour
	- [ ] 1 egg
	- [ ] 1/4 tsp salt
	- [ ] tangzhong
- [ ] almond filling
	- [ ] 1/2 cup butter
	- [ ] 100g granulated sugar
	- [ ] 140g almond flour
	- [ ] 1 tsp vanilla extract
	- [ ] 1/2 tsp almond extract
	- [ ] 1 egg
	- [ ] 1/4 tsp salt
- [ ] assembly
	- [ ] knead complete dough until fully combined
	- [ ] add 1/2 cup butter in 2 parts
	- [ ] knead until smooth, glossy
	- [ ] let rise for 1 hour
	- [ ] divide into 12 balls and let rise for 45 minutes
	- [ ] press divot into center of each ball
	- [ ] brush with egg wash (1 egg)
	- [ ] add almond filling
	- [ ] top with roasted almonds
- [ ] bake
	- [ ] 13-15 minutes @ 375°F
## ingredients
tags: #ap_flour, #milk, #instant_yeast, #granulated_sugar, #egg, #salt, #butter, #almond_flour, #vanilla_extract, #almond_extract, #almond
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