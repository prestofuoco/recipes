- [ ] filling
	- [ ] 400g extra-firm tofu, cut into slabs & seared
	- [ ] 15g soy sauce
	- [ ] 1/2 juiced lemon
	- [ ] 1 tsp ginger
- [ ] inclusions
	- [ ] 1 large cucumber, thinly sliced
	- [ ] 1/2 red onion, thinly sliced
	- [ ] 1 tbsp vinegar
- [ ] assembly
	- [ ] 6 slices whole wheat bread
	- [ ] 30g greek yogurt
	- [ ] 5g dijon mustard
	- [ ] 2 cups spring mix
## ingredients
tags: #tofu, #soy_sauce, #lemon, #ginger, #cucumber, #red_onion, #vinegar, #bread, #greek_yogurt, #dijon_mustard
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
