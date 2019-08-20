# Coding the right way

Often development process becomes primarily focused on if **IT WORKED** rather than if **IT WAS DONE RIGHT**.
As days pass by, project grows in volume, bit's of cleanup and refactoring tasks pile up requiring a huge refactoring initiative in future.
Taking a cleanup initiative at the end of every project is not possible due to time and other constraints.
Developer awareness can prevent it from happening in the first place.

## Objective

The objective of this document is to raise developer awareness on coding conventions and better coding practices (do's and don't while writing code) and thus preventing massive cleanup effort later when the project grows.

## Disclaimer

- All code snippets presented here are imaginary and only for citation.
- None of the code were taken from any existing project.
- I would highly appreciate any correction provided with reference.

## Follow standard and conventions

**Convension:** Convensions are ways to do specific task.  
**Standard:** Standard is a convention which is:

  1. Prescribed by the language
  2. Adopted by the community
  3. Used by notable open source projects
  4. Decided by your team

For example we can look into naming conventions in different programming languages:

### 1. Prescribed by the language

Visual Studio suggests following naming convention for C# applications:

- Classes/Types should be in titlecase, e.g `QuadrupedAnimal`
- Variable names should be in camelcase, e.g `quadrupedAnimal`
- Class methods should be in titlecase, e.g `quadrupedAnimal.BarkTwice()`

```C#
Animal animal = new Animal();
QuadrupedAnimal quadrupedAnimal = new QuadrupedAnimal();
quadrupedAnimal.BarkTwice();
```

### 2. Adopted by the community

Python community has Pep8 specification for writing python applications:

- Classes/Types should be in titlecase, e.g `QuadrupedAnimal`
- Variable & Function names should be in snakecase, e.g `animal_child.bark_twice()`

```py
animal = Animal()
animal_child = QuadrupedAnimal()
animal_child.bark_twice()
```

### 3. Used by notable open source projects

JavaScript/Typescript specification used by Google, Microsoft & Facebook team in renowned open source projects:

- Classes/Types should be in titlecase, e.g `QuadrupedAnimal`
- Variable names should be in camelcase, e.g `quadrupedAnimal`
- Class methods should be in camelcase, e.g `quadrupedAnimal.barkTwice()`

```js
let animal = new Animal();
let quadrupedAnimal = new QuadrupedAnimal();
quadrupedAnimal.barkTwice();
```

### 4. Decided by your team

In case of JSON key naming, your team has to decide which convention to follow as developers of different platform has their own preferences.

```json
{
  "camelCase": "Used by JavaScript developers and Google Team",
  "TitleCase": "Used by C# developers and AWS",
  "snake_case": "PHP & Python developers",
  "kebab-case": "I'm just curious if anyone uses it",
}
```

## Avoid common coding mishaps

### Redundant prefixes

I always wondered what is so special about `id` and `status` that only they contain `person` prefix in object definitions.

```plain
Person
- person_id
- department_id
- name
- age
- address
- person_status
```

I would suggest to follow only one of the following to maintain consistency:

```plain
Person                           Person (kidding ;)
- id                             - person_id
- department_id                  - person_department_id
- name                           - person_name
- age                            - person_age
- address                        - person_address
- status                         - person_status
```

### Redundant HTML attributes

Do all HTML elements need and ID?

```html
<body id="body">
  <header id="header">
    <nav id="nav">
      <any-thing id="any-thing"></any-thing>
      <button id="button" type="submit">OK</button>
    </nav>
  </header>
</body>
```

We all copy-paste from stack-overflow at times, but a little clean-up only takes few seconds right?

Even a button does not require `type=submit` (I know there are exceptions ;) You can simply write:

```html
<button>OK</button>
```

Prefer writing only what is needed, so developers can focus on what matters.

### Explanatory comments

Sometimes we try to describe every line of our code with comments.

```js
let accessToken = 'xxxxxxx'; // cognito access token
let userGroup = 'yyyyyy';    // cognito user group

function print(){}           // prints nothing
```

Comments are not meant to describe your code. If you need comments to describe your code, you are not writing it right.

Use self-explanatory variable/function names instead:

```js
let cognitoAccessToken = 'xxxxxxx';
let cognitoUserType = 'xxxxxxx';

function printNothing(){}
```

### Commenting everything

Instead of writing useless comments:

```py
## add function
def add(a, b):
  return a + b

## substract function
def substract(a, b):
  return a + b
```

Write doc-strings instead (for python):

```py
def add(a, b):
  """ Returns the sum to 2 numbers """
  return a + b
```

Write annotation comments instead (for JavaScript):

```js
/**
  * Returns the sum to 2 numbers
  */
function add(a, b) {
  return a + b;
}
```

### Boundary marker comments

This is how comments make me SAD :(

```html
<!-- body start -->
<body>
  <!-- header start -->
  <header>
    <!-- nav start -->
    <nav>
    </nav>
    <!-- nav end -->
  </header>
  <!-- header end -->
</body>
<!-- body end -->
```

To me the following code looks way more easier to understand while the above code needs clean-up.

```html
<body>
  <header>
    <nav>
    </nav>
  </header>
</body>
```

### Back-up comments

Keeping backup of old code in comments will just bloat your codebase.
Always keep codebase clean removing stale and old code.
It you need it later, Git is there.

```py
def update(box):
  # box.check()
  # box.update()
  box.checkAndUpdate()
```

### Copy paste blunder

Often while copy-pasting code we tend to change only what has to be changed to make it work, but forget to change what should be changed to make it meaningful.

```py
for apple in apples:
  print(apple.batch_id)
  print(apple.variety_id)
  print(apple.weight)

for apple in oranges:
  print(apple.batch_id)
  print(apple.variety_id)
  print(apple.weight)
```

### Leaving behind stray code

Debugging based on printing and logging is not appreciated at all,
you should use proper debug tools.
And what you definitely don't wanna do is leaving behind stray code.

```js
function hello() {
  let fisrtNumber = 10;
  console.log("initialized fisrtNumber");
  let secondNumber = 20;
  console.log("initialized secondNumber");
  return fisrtNumber + secondNumber;
  console.log("why this line is not logging!!!");
}
```

```py
if __name__ == "__main__":
  fisrt_number = 10
  second_number = 20
  print("OK")
```

## What should we do

This is highly opinionated and varies environment to environment.
Developer's need to sit together to define standard for the team.
These are few points I always suggest my team to follow:

### When should you write comments

- Write Annotation Comments.
- Use TODO Comments:

    ```py
    def jump():
      # TODO: add doc-string
      print("I can't")
    ```

- You can write warning comments when there is a concern of accidental modification:

    ```py
    def update(box):
      box.save()
      box.save()
      # you have to save twice, thanks to me :)
      # otherwise DB will not be updated.
    ```

- Use comments only when you need it, I would say the less, the better.

### When should you avoid comments

- Don't use comment to describe your code, write self-explanatory code.
- Don't use comment to back-up your code, use git instead.
- Don't use comment to to mark bundaries, use an IDE instead.
- Comments are meant to be READ by the developer, so write something HELPFUL.

### What case to use where no standard is defined

You can use kebab-case where no standard is defined.

- URL: `https://ala-uddin.com/my-profile`
- File/Folder Name: `graaho-logo.jpg`
- Template Name: `profile-edit.html`

### Follow convention properly

You can use linters to make it easier to stick to conventions.

```py
def add(a, b):
  """ Single NewLine before/after function """
  return a + b

def substract(a, b):
  """ Single NewLine before/after function """
  return a - b


class Math:
  """ Double NewLine before/after class, single newline after class doc-string """

  def multiply(a, b):
    return a * b
  
  class Anything:
    """ Single NewLine before/after nested class """
    pass

  def devide(a, b):
    return a * b


def splitting_function_codes_into_blocks():
  """ Pep8 won't stop you from doing it, but should you? """

  first_number = 10
  second_number = 20

  return first_number + second_number
```

If your function becomes bloated requiring function code to be grouped into separate blocks, splitting into multiple functions can be a better solution.

### Clean up as you go

- Clean up your code as you go developing the project side by side. Little fixes daily can prevent enormous fixes in the future.
- After you make it work, spend few seconds to clean-up what have you done before pushing the commit.
- Spend few minutes daily to review, restructure, re-order, clean up the parts of the codebase containig commits you authored.
- PEER CODE REVIEW before merging the commit can significantly upgrade the code quality of every developer.

## Acknowledgements

This document was written while I was working at [GRAAHO](http://www.graaho.com/) and was considered a must read for anyone who joins the team saving us few minutes of communicating the development ethics we follow.
It is published under MIT licence, you can fork it to define your coding guidelines for your team.
