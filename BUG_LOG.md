# Docking Bay Bug Log

**Name:** Zackary Santos

Log **every** bug as you fix it, one row per bug. There are **15**: 5 syntax, 4 runtime, 6 logic.

- **File**: which file the bug was in, e.g. `Services/ShipService.cs`
- **Line**: the line number where you made the fix
- **Kind**: `Syntax`, `Runtime` or `Logic`
- **What was wrong**: what the code did, and how you noticed (the build error, the exception, or the wrong result in Postman)
- **How I fixed it**: exactly what you changed

## Example (not one of the 15)

| # | File | Line | Kind | What was wrong | How I fixed it |
|---|------|------|------|----------------|----------------|
| 0 | `Services/ExampleService.cs` | 22 | Logic | `GET /api/example/cheapest` returned the **most** expensive item. The list was sorted with `OrderByDescending(i => i.Price)`, so the first item was the priciest. | Changed `OrderByDescending` to `OrderBy`. |

## My bugs

| # | File | Line | Kind | What was wrong | How I fixed it |
|---|------|------|------|----------------|----------------|
| 1 | PioltsController.cs | 13 | Syntax | PilotsController was spelled as "PilotController" causing the code to not run as it did not recognize the name | changed the name back to "PilotController"
| 2 | ShipsController.cs | 32 | Syntax | [HttpGet("{id}")] was missing an end bracket | added the end bracket
| 3 | Ship.cs | 6 | Syntax |  public string Name { get; set; } = string.Empty was missing a colon at the end of the line | added a colon to the end of the code line
| 4 | IPilotService.cs | 9 | Syntax | List<Pilot> GetOnDuty(); was not capitalized | Made List Capitalized
| 5 | ShipService.cs | 10 | Syntax | Name = "Iron Comet" did not have a comma after it, causing it to result in an error for the item in the list | added a comma after it to fix the list
| 6 | program.cs | 8 | Runtime | builder.Services.AddScoped had IShipService and ShipService a second time instead of IPilotService and PilotService | replaced IShipService and Ship Service with IPilotService and PilotService
| 7 | ShipsController.cs | 37 | Logic | if statement had != instead of ==, causing entering the correct Id to return as a NotFound Message | changed != to ==
| 8 | ShipService.cs | 54 | Logic | ship.FuelPercent would add 100 to fuel instead of making it equal to 100 | Changed the statment to only include an = so it sets the fuel to 100 when refuel happens
| 9 | ShipServices.cs | 67 | Runtime | removed = true was causing the program to have a error because it was being changed while in the for loop | changed the code line to "return true;"
| 10 | PilotsController.cs | 62 | Logic | if statement would allow 0 hours to be logged in because the if statement used < instead of <= | changed < to <=
| 11 | ShipsController.cs | 49 | Logic | return statement was using the wrong response code. It was using Ok instead of CreatedAtAction, which is used for adding to database | changed Return Ok() to  Return CreatedAtAction(nameof(GetById), new {id = created.Id}, created);
| 12 | PilotService.cs | 49 | Runtime | LogHours did not have an if statement to check for null, resulting in a runtime error when entering in an unkown id | added an if statement that checked for null and returns false if null is detected
| 13 | ShipService.cs | 21 | Runtime | return was not checking for Null when a null value was inputted, resulting in a crash because .First does not check for Null unlike .FirstOrDefault | replaced .First with .FirstOrDefault
| 14 | PilotService.cs | 38 | Logic | When creating a new Pilot, the new Pilot's Id was bugged because there was no code that would allow the next pilot to be incremented | changed pilot.Id = _nextId; to pilot.Id = _nextId++; which fixed the error
| 15 | ShipService.cs | 14 | Logic | newId was not able to count past 3, causing new ships to have an Id of 3. | Added static int newId = 4 under the list of ships so that newId can make Ids higher than 3.

## Tally

| Kind | Found |
|------|-------|
| Syntax | 5 / 5 |
| Runtime | 4 / 4 |
| Logic | 6 / 6 |

## Reflection

Answer each in 2–3 sentences.

1. Which bug took you the longest to find? What finally led you to it?
## The Bug that I had the most difficulty with was in ShipsController.cs where I had to fix a Logic Error for when an error when I had to enter an ID. I was able to fix it through comparing the ShipsController Code to PilotsController.cs and I was able to see what was wrong since both code was simmilar to each other.

2. Pick one **runtime** error. What exception did it throw, and how did the error message help you find the line?

## When testing inputting hours for pilots, I entered a false number and I was given the exception "System.NullReferenceException". This told me that I needed to add a null check to the code. I found the line by going to PilotService.cs and found where I needed to put the null check when LogHours was giving rules

3. `DELETE /api/ships/3` crashed with `Collection was modified`. Why can't a `foreach` loop keep going after you remove something from the list it's looping over?

## The reason why a foreach loop cant continue is because since a foreach loop goes through everything within a collection, something being altered in it will cause the compiler to become confused. Then a Runtime error will happen because the compiler will not be able to continue. 

4. Every `/api/pilots` request crashed until you fixed one line in `Program.cs`. Explain what dependency injection was trying to do and why it failed.

## The dependancy injection was trying to connect to the IPilotServace interface so it can get access to the rules in it. The Reason why it was failing was because PilotsController was misspelled, making the compiler see PilotsController as Invalid.

5. Several logic bugs were a single character, like `!=` versus `==`, `<` versus `<=`, or
   `=` versus `+=`. Why doesn't the compiler catch these?

## The Reason why the compiler couldnt catch them is because the code can technically still work despite it not being the indended way for it to work from the Developer. This is also why the compiler was also not able to see these as runtime errors as well.

6. Some bugs hid until you fixed a different one. Give one example.

## I had to first fix a colon error in Ship.cs to finish a line. After that A new error appeared in ShipService.cs where I had to fix a comma error that then appeared.