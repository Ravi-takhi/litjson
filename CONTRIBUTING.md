# Intoduction
## Project Name: LitJson
The LitJSON community code project is an open-source initiative aimed at developing and maintaining a lightweight and efficient JSON library for the .NET platform. Built upon the principles of simplicity, performance, and ease of use, LitJSON provides developers with a robust toolset for working with JSON data in their .NET applications.
### Key Feaures
* Simplifies JSON data handling: LitJSON simplifies the process of parsing and serializing JSON data, allowing developers to focus on building robust applications.
* Improves performance: With its lightweight design and optimized performance, LitJSON ensures fast and efficient JSON processing, even with large datasets.
* Enhances productivity: By providing a user-friendly API and comprehensive documentation, LitJSON helps developers save time and effort during the development process.
### Issue Summary
This issue, raised by corbinyo, is about making a change in LitJSON. Currently, when using the JsonMapper.ToObject method to turn JSON into objects in .NET, null values in the JSON data become null objects in the resulting .NET objects. But sometimes, we don't want these null values. We'd prefer to skip them to make things simpler.

The request is to add a feature that lets us tell LitJSON to ignore these null values when turning JSON into objects. This would make working with JSON data in .NET even easier and more efficient.
