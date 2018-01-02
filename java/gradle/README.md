## Gradle
> Notes taken from [Pluralsight's Gradle Fundamentals course](https://app.pluralsight.com/library/courses/gradle-fundamentals/table-of-contents).

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
		- Executes any code in the task that's not the action (e.g. setting a description)
	1. Execution phase

## Sample `build.gradle`
> Run `gradle tasks` to see a list of tasks and use `gradle Task1` to run a specific task.

```
project.task("Task1")
task("Task2")
task "Task3"
task Task4

Task4.description = "Task 4 description"
Task4.doLast {println "This is Task 4"}

Task3 << {println "This is Task 3"}

task Task5 << {println "This is Task 5"}
Task5 << {println "Another closure for Task 5"}
```
