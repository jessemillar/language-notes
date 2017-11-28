## General Notes
### Interface
- An interface is essentially a contract that a class will follow in order to standardize an API (think header file)

### Spring
- Spring is largely used for inversion of control (IoC)

#### Inversion of Control
- If a function needs a dependency, that dependency should be passed in as an argument so that there aren't tight dependencies anywhere:
- Instead of:
	```
	public class TextEditor {
		private SpellChecker checker;

		public TextEditor() {
			this.checker = new SpellChecker();
		}
	}
	```
	...do...
	```
	public class TextEditor {

		private IocSpellChecker checker;

		public TextEditor(IocSpellChecker checker) {
			this.checker = checker;
		}
	}
	```
