# Intoduction
## Project Name: LitJson
The LitJSON community code project is an open-source initiative aimed at developing and maintaining a lightweight and efficient JSON library for the .NET platform. Built upon the principles of simplicity, performance, and ease of use, LitJSON provides developers with a robust toolset for working with JSON data in their .NET applications.
### Key Feaures
* Simplifies JSON data handling: LitJSON simplifies the process of parsing and serializing JSON data, allowing developers to focus on building robust applications.
* Improves performance: With its lightweight design and optimized performance, LitJSON ensures fast and efficient JSON processing, even with large datasets.
* Enhances productivity: By providing a user-friendly API and comprehensive documentation, LitJSON helps developers save time and effort during the development process.
### Link
https://github.com/Ravi-takhi/litjson/tree/Ravi-Dev-Branch
### Summary of issues examined
This issue, raised by corbinyo, to find a way to handle null values during deserialization. The task involved ensuring that null values from JSON data were ignored when converting it into C# objects. He is using the Litjson library for the serialization and deserialization.
### Detailed discussion of issues contributed to
I worked on a specific issue related to ignoring null values during deserialization with LitJSON. My goal was to prevent null values in JSON from being assigned to object properties during the conversion process. I explored different methods, including manually checking for null values, creating custom importers, and modifying the JSON data before deserialization. Ultimately, I found a solution by adjusting the JSON string before parsing it into objects, effectively solving the problem even though LitJSON doesn't have a built-in feature for this. I also looked into the other libraries such as Newtonsoft, they provides some in-built functionalities to ingnore or skip the null values during the serialization data.
#### Example for skip null value while deserialization
``` csharp
using LitJson;
using System;

public class Student
{
    public int Id { get; set; }
    public string Name { get; set; }
    public int? Age { get; set; } // Nullable int for handling null values
}

class Program
{
    static void Main(string[] args)
    {
        string json = "{\"Id\": 1, \"Name\": \"John\", \"Age\": null }"; // JSON string with null value for Age

        JsonData jsonData = JsonMapper.ToObject(json);

        Student std = new Student();

        if (jsonData["Id"] != null)
            std.Id = (int)jsonData["Id"];

        if (jsonData["Name"] != null)
            std.Name = (string)jsonData["Name"];

        // Handle null value for Age
        if (jsonData["Age"] != null)
        {
            if (jsonData["Age"].IsInt) // Check if the value is an integer
                std.Age = (int)jsonData["Age"];
            else
                std.Age = null;
        }

        Console.WriteLine($"Id: {std.Id}, Name: {std.Name}, Age: {(std.Age.HasValue ? std.Age.ToString() : "N/A")}");
    }
}
```
### Code review and outcomes
#### Code review
The initial version of the program effectively handles null values during JSON deserialization into a Student object. However, it could be improved for better readability and maintainability. The improved version introduces a method called RemoveNullValues to handle null values more efficiently. By encapsulating the null value removal logic, the code becomes simpler and easier to maintain. The updated version of the code is definitely a step forward. In the old version, fetching values from the JSON data required mentioning variable names explicitly. This could be troublesome if we add more variables to the Student class later on. However, the new version has a neat function called RemoveNullValues that takes care of this. Now, we don't need to worry about manually handling each variable. This makes the code simpler and more flexible, which is great for maintaining and modifying the Student class in the future. Additionally, a proposed enhancement suggests introducing a method named DeserializeNonNullValues to further streamline the deserialization process. Overall, these changes enhance the readability, maintainability, and robustness of the code, ensuring it adheres to best practices in software development.
#### Outcome
Upon receiving feedback from Katrina, I carefully considered her suggestions and realized the importance of simplifying and enhancing the code. By implementing the improvements suggested by Katrina, I was able to make the code more readable, maintainable, and flexible. This highlights the value of feedback in driving positive changes and improving overall code quality.
### Updated version
``` csharp
public class Student
{
    public int Id { get; set; }
    public string Name { get; set; }
    public int? Age { get; set; } // Nullable int for handling null values
}

class Program
{
    static void Main(string[] args)
    {
        string json = "{\"Id\": 1, \"Name\": \"John\", \"Age\": null }"; // JSON string with null value for Age

        // Remove or replace null values from the JSON string
        json = RemoveNullValues(json);

        Student std = JsonMapper.ToObject<Student>(json);

        Console.WriteLine($"Id: {std.Id}, Name: {std.Name}, Age: {(std.Age.HasValue ? std.Age.ToString() : "N/A")}");
    }

    static string RemoveNullValues(string json)
    {
        // Replace "null" with an empty string
        return Regex.Replace(json, "\"[^\"]+\":\\s*null,?", "");
    }
}
```
