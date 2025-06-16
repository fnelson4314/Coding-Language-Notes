# Powershell

### Basics

- Comments are done with the hashtag(#)
- Cmdlets are things like Write-Host that are native PowerShell commands
  - These follow a **Verb-noun** naming convention
  - To see a list of all the cmdlets, you can enter **Get-Command -CommandTyper Cmdlet** into the shell
- If you would like to see the syntax/options of a certain cmdlet, you can do **get-Hel cmdlet -Full**
- **|** can be used to pipe the output of one things into the input of another
  - **"May the force be with you!" | Out-File forcewithwho.txt**
- **`n** can be used to do a newline
- In order to evaluate expressions inside double quotes strings (""), you must put them inside a **$()**
  - **Write-Host "Could not parse log entries between i and $($i + 1)."**


### Random Flags/Params

- The -f flag can be used to do a format string
  - **$elapsedString = "{0}mo {1}d {2}h {3}m" -f $months, $days, $hours, $minutes**


### Important cmdlets
- **Write-Host** – Prints to the command line
  - **Write-Host “Hello World” -NoNewline**
  - This automatically adds a newline at the end as well
  - Write-Host takes many parameter options, one of them being -NoNewline which removes the default newline after writing to the host
- **Read-Host**  - Gets input from the command line
  - **Read-Host “Full path to the file with list of hosts”**
- **Add-Content** – Adds content to the specified items, such as adding words to a file
  - **Add-Content -Path <Path to add to> -Value <Values to add>**
- **Select-Object** – Can be used to grab properties from an object
  - For example, Invoke-WebRequest returns a WebResponseObject which has many properties in it and Select-Object can grab any of those properties to use
  - **$response = Invoke-WebRequest -Uri $URL -Credential $basicCreds | Select-Object -Expand Content**
  - **Select-Object -Last 2** grabs the last two entries from the data
- **Get-Content** – Grabs content from the specified location
  - **Get-Content -Path $logFile**
- **Compare-Object** – Allows you to compare two objects 
  - **Compare-Object -ReferenceObject $File1 -DifferenceObject $File2**
- **Format-Table** – Formats the data as a table
  - **Get-Host | Format-Table <param>**
  - Can also add only certain keys that you want shown
    - **$data | Format-Table name, status, totalAgents, activeAgents**
- **Invoke-WebRequest** – Gets content from a webpage on the internet. A URL needs to be given along with the -Uri param. Returns a WebResponseObject that has information such as:
  - **StatusCode**: The HTTP status code (e.g., 200, 404)
  - **Content**: The body of the response (HTML, FSON, XML, etc.)
  - **Headers**: The HTTP headers returned by the server
  - **RawContent** – The full raw response as a string.
  - **Links, Forms, Images** – Parsed HTML elements
  - Can be used like: **WebResponseObject.Content**
  - **Invoke-WebRequest -Uri $TestURL -Credentials $basicCreds**
- **ConvertFrom-Json** – Used to convert a JSON-formatted string to a custom object or hash table so that data can be accessed
  - **$data = $response.Content | ConvertFrom-Json**
- **Get-Date** – Gets the current date and time
  - **$timestamp = Get-Date -Format “yyyy-MM-dd HH:mm:ss”**
- **Where-Object** – Selects objects from a collection based on their property values
  - **Where-Object {$_.status -eq “Online” }**
  - **$_** refers to the current object being piped
- **ForEach-Object** – Performs an operation against each item in a collection of input objects
  - **ForEach-Object {}**
- **Add-Member** – Adds custom properties and methods to an instance of an object
  - **$_ | Add-Member -NotePropertyName totalTimeDeployed -NotePropertyValue $elapsedString -Force**
- **Export-Csv** – Converts objects into a series of character-separated value strings and saves the strings to a file
  - **Export-Csv -Path “UCD_Agents.csv” -NoTypeInformation**
  - The **-NoTypeInformation** removes the #TYPE header from the file
- **Group-Object** – Groups objects that contain the same value for specified properties. Returns a table with one row for each property value and a column for each property.
  - **$versionSummary = $data | Group-Object version**
- **PSCustomObject** – Used to create custom objects with properties and values
  - **$person = [PSCustomObject]@{**
    - **FirstName = “John”**
    - **LastName = “Doe”**
    - **Age = 30**
    - **City = “Phoenix”**
  - **}**
- **Get-Member** – Gets the properties and methods of objects
  - Use **-MemberType Property** to get the properties
  - Use **-MemberType Methods** to get all methods
  - Do Get-Member by itself to get everything
  - **$data | Get-Member -MemberType Property | Out-GridView**



### Variables
- Variables can be invoked with a dollar sign($)
  - **$FavCharacter = “Spongebob”**



### Arrays

- Creating an array can be done with the @ sign
  - **$jedi = @(‘apple’, ‘pear’, ‘banana’)**
- You can index like any other language(**$jedi[0]**)
- You can add to an array with the += operator
  - **$jedi += “orange”**


 
### Hash Tables(Dictionaries)
- Syntax is the same as an array, but with curly brackets({})
  - **$Fellowship = @{“Wizard” = “Gandalf”; “Hobbit” = “Frodo”; “Elf = “Legolas” }**
- To add to a hash table, you can use the **.Add()** function
  - **$Fellowship.Add(“Dwarf”, “Gimli”)**
•	To set/update an item, use the .Set_Item() function
o	$Fellowship.Set_Item(“Dwarf”, “Bilbo”)
•	To get data from a hash table
o	$Fellowship.”Dwarf” or you can do normally $Fellowship[“Dwarf”]
•	To remove data from a data table
o	$Fellowship.Remove(“Dwarf”)


Conditional Statements

•	To do an if-else statement:
o	$PokemonNum = 25
o	If ($PokemonNum -ge 0 -and $PokemonNum -le 151) {Write-Host “The same!”}
o	Elseif ($PokemonNum -ge 152 -and $PokemonNum -le 251) {Write-Host “Something”}
o	Else {Write-Host “Not the same!}
•	Switch statement:
o	Switch ($outputType.ToLower()) {
	“table” {}
	“json” {}
	Default {}
o	}



Loops
•	For Loops:
o	For($counter = 0; $counter -le 3; $counter++) {
•	For each loop:
o	Foreach($peep in $HaloPeeps) {
•	While loop:
o	While($counter -ne 6) {
