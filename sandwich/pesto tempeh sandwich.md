- [ ] filling
	- [ ] 8oz tempeh (steamed 10 min. then crumbled)
	- [ ] 120g greek yogurt
	- [ ] 45g pesto
	- [ ] 5g dijon mustard
	- [ ] 1/2 juiced lemon
	- [ ] salt & pepper
- [ ] inclusions
	- [ ] 2 stalks celery, finely diced
	- [ ] 1/4 red onion, finely diced
	- [ ] (optional) 40g feta cheese, crumbled
- [ ] assembly
	- [ ] 6 slices whole wheat bread
	- [ ] 1 large cucumber, thinly sliced
	- [ ] 2 cups spring mix
	- [ ] (optional) hummus
## ingredients
tags: #tempeh, #greek_yogurt, #pesto, #dijon_mustard, #lemon, #celery, #red_onion, #feta_cheese, #bread, #cucumber, #hummus
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
