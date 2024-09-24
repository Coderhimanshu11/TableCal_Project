CSV Processing API in Spring Boot
Overview
This project is a Spring Boot-based application that provides an API for processing CSV strings. The API reads and processes CSV inputs, evaluates formulas or values, and outputs the results in a formatted table.
Features
•	Accepts CSV data through a REST API.
•	Parses the CSV input into rows and columns.
•	Processes and evaluates both numeric values and simple arithmetic formulas (e.g., =A1+B1).
•	Returns the CSV result in a structured tabular format.
Technologies Used
•	Java 8+: Core language.
•	Spring Boot: For building the REST API.
•	Lombok: For reducing boilerplate code.
•	Maven: Dependency management and build automation.
•	HTTP: RESTful service using Spring's RestController.
API Endpoints
1. Add CSV Data
•	URL: /csv/add
•	Method: POST
•	Request Body:
o	JSON object containing the CSV data.
o	Example:
json
{
  "strCsv": "A1: 1, B1: 2, C1: 3, A2: 4, B2: 5, C2: =A1+B1, A3: =A1+A2, B3: 8, C3: =B2+C1"
}
•	Response:
o	On success: A string representation of the CSV table with the evaluated results.
|  | A  | B  | C  |
| --- | --- | --- | --- |
| 1 | 1.0 | 2.0 | 3.0 |
| 2 | 4.0 | 5.0 | 3.0 |
| 3 | 5.0 | 8.0 | 8.0 |
o	On failure: Error message detailing the issue with the CSV format.
Code Structure
1. Controller
•	Handles incoming REST requests.
@PostMapping("/add")
public ResponseEntity<String> addCsv(@RequestBody CSVRequestDto csvRequestDto) {
    String result = csvService.processCSV(csvRequestDto.getStrCsv());
    return ResponseEntity.ok(result);
}
2. CSVRequestDto
•	DTO class for capturing the incoming CSV string in the request body.
•	Fields:
o	strCsv: The raw CSV string input.
3. CSVService
•	Contains business logic for processing CSV data.
•	Splits the input CSV string into rows and cells.
•	Evaluates cell values or simple arithmetic formulas.
•	Constructs and returns the output in tabular format.
java
public String processCSV(String csvStr) {
    String[] rows = csvStr.split(", ");
    return outputCsv;
}
4. CSV Processing Logic
•	Evaluate Cell Values: Checks if the cell contains a formula (=A1+B1), evaluates it, and stores the result.
•	Evaluate Formula: Parses simple arithmetic expressions like =A1+B1, retrieves the values from corresponding cells, and computes the result.
Example Input and Output
Input
json
{
  "strCsv": "A1: 1, B1: 2, C1: 3, A2: 4, B2: 5, C2: =A1+B1, A3: =A1+A2, B3: 8, C3: =B2+C1"
}
Output
|  | A  | B  | C  |
| --- | --- | --- | --- |
| 1 | 1.0 | 2.0 | 3.0 |
| 2 | 4.0 | 5.0 | 3.0 |
| 3 | 5.0 | 8.0 | 8.0 |
Running the Application
1.	Clone the Repository:
bash
git clone https://github.com/Coderhimanshu11/TableCal_Project
2.	Build and Run the Application:
bash
mvn spring-boot:run
Error Handling
•	The API responds with appropriate error messages when:
o	The CSV format is invalid.
o	A cell contains incorrect or non-parsable data.
o	Example error message:
json
{
  "message": "Error csv: Invalid format for entry: A1: 1 B1 2"
}
Conclusion
This project demonstrates how to build a CSV processing API using Spring Boot. It parses CSV input strings, evaluates formulas, and outputs the final results in a tabular format, which can be used for various calculations or further processing.
________________________________________

