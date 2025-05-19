---
project: 
status: In Progress
priority: Medium
due: 
tasks:
---
## Описание проекта


```dataviewjs
const currentProject = "{{tp_file_name}}"; // Получаем все страницы в папке "Tasks" и фильтруем по проекту

const pages = dv.pages('"Tasks"').where(p =>
	Array.isArray(p.project) ? p.project.some(proj => proj.path.endsWith(currentProject + ".md")) : p.project?.path.endsWith(currentProject + ".md")
);

dv.table(
	[ "<b style='color: #777; font-size: 14px;'>Task</b>",
	"<b style='color: #777; font-size: 14px;'>Project</b>",
	"<b style='color: #777; font-size: 14px;'>Due Date</b>"
	],

	pages.map(p => [ `[[${p.file.name}]]`, // Ссылка на задачу
	Array.isArray(p.project)
		? p.project.map(proj =>
		`[[${proj.path}]]`).join(", ") // Выводим ссылки на проекты
		: (p.project ? `[[${p.project.path}]]`
		: 'No project'),
	p.due
		? `<span style="color: #0077b6;">${new Date(p.due.toISODate()).toLocaleDateString("en-GB")}</span>`
		: 'No due date'
	])
);
```