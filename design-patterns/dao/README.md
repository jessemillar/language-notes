## DAO
- "...an object that provides an abstract interface to some type of database or other persistence mechanism."
- It's basically the same thing as the reader/writer pattern we're using at Walmart for grocery pickup
- For example (https://stackoverflow.com/a/19154487/3958178), you can have a class like this:
	```
	public class Employee {
		private int id;
		private String name;

		public int getId() {
			return id;
		}

		public void setId(int id) {
			this.id = id;
		}

		public String getName() {
			return name;
		}

		public void setName(String name) {
			this.name = name;
		}
	}
	```
	...with a DAO interface like this...
	```
	interface EmployeeDAO {
		List<Employee> findAll();
		List<Employee> findById();
		List<Employee> findByName();
		boolean insertEmployee(Employee employee);
		boolean updateEmployee(Employee employee);
		boolean deleteEmployee(Employee employee);
	}
	```
