# aurpublish details

I update aur packages via aurpublish, the method to update it via it is listed below:

- Create a parent folder via `mkdir <folder-name>`
- Then goto that folder via `cd <folder-name>`
- `git init` inside that folder
- Then `git add.`
- Then `git commit -m "Commit message"`
- Run `aurpublish setup` command
- Run `aurpublish -p <folder-name>`
- Run `cd <folder-name>`
- Run `git add .`
- Run `git commit`
- Run `aurpublish <package-name> `
