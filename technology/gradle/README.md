## Gradle
> Notes taken from [Pluralsight's Gradle Fundamentals course](https://app.pluralsight.com/library/courses/gradle-fundamentals/table-of-contents).

- Gradle is largely used for Java but can be used for projects in any language
- Gradle files (`build.gradle`) are written in [Groovy](http://groovy-lang.org/)
	- Groovy is object oriented with `project` being the top-level object
- Gradle has tasks
	- Tasks have actions
		- You can easily append to an existing task by simply adding a new Groovy closure (which is just code in curly braces)
			- Anything appended with `<<` gets added to the `doLast` method
		- Task actions go inside methods/functions such as the default `doFirst` and `doLast` methods
			- `doLast` is part of every task and it's the last thing that runs
- Gradle has multiple build phases
	1. Initialization phase
		- Used to configure multi project builds
	1. Configuration phase
		- Executes any code in the task that's not the action (e.g. setting a description or creating task dependency graphs)
	1. Execution phase
- Gradle tasks can have dependencies on other tasks via `dependsOn`
	- You can define multiple dependencies on one line by comma separating them
	- By default, the order that dependencies run in is decided by Gradle
		- `shouldRunAfter`, `mustRunAfter`, and `finalizedBy` (incubating in 2.6) allow us to set certain orders for dependencies
			- `shouldRunAfter` ignores circular dependencies
- Use the `def` keyword to define local variables
	- Reference them by preceding their name with a `$`
	- You can also set "extended" properties that can be used in multiple places

## Sample `build.gradle`
> Run `gradle tasks` to see a list of tasks and use `gradle Task1` to run a specific task.

```
def projectVersion = "2.0"

project.task("Task1")
task("Task2")
task "Task3"
task Task4

Task4.description = "Task 4 description"
Task4.doLast {println "This is Task 4 $projectVersion"}

Task3 << {println "This is Task 3"}

task Task5 << {println "This is Task 5"}
Task5 << {println "Another closure for Task 5"}
```
