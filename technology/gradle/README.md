## Gradle
> Notes taken while watching [Pluralsight's Gradle Fundamentals course](https://app.pluralsight.com/library/courses/gradle-fundamentals/table-of-contents).

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
- Typed tasks allow us to reuse tasks and accept input
	- Good uses of typed tasks are copying and/or zipping files
	- You can use `with` to create specifications that can be used to configure multiple tasks
- Plugins are added to a Gradle file with the `apply` keyword
- `SourceSets` can allow us to define our own code layouts different from the Maven/Gradle standard with `src/java`/`src/test`/etc.

## Sample `build.gradle`
> Run `gradle tasks` to see a list of tasks and use `gradle Task1` to run a specific task.

```
apply plugin: "java"

// Set a version for the Java plugin
version = "1.0"

// Demonstrate local variables
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

// Demonstrate a typed task that copies files
task copyImages (type: Copy) {
	// Exclude files by exact name
	exclude "IMG_0052.JPG", "IMG_004.JPG"
	// Exclude files via a Groovy regex-like method
	exclude {it.file.name.startsWith("IMG")}
	from "src"
	into "dest"
}
```
