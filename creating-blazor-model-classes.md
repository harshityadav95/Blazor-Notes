# Creating blazor model classes

As we progress through this course we will be building Employee management system that allows us to Create, Read, Update and Delete employees. The following are the model classes we need.

1. Employee
2. Department
3. Gender

```text
// Employee class

public class Employee
{
    public int EmployeeId { get; set; }
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public string Email { get; set; }
    public DateTime DateOfBrith { get; set; }
    public Gender Gender { get; set; }
    public Department Department { get; set; }
    public string PhotoPath { get; set; }
}

// Gender Enum

public enum Gender
{
    Male,
    Female,
    Other
}

// Department Class

public class Department
{
    public int DepartmentId { get; set; }
    public string DepartmentName { get; set; }
}
```



