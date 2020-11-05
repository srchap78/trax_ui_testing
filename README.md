# _**UI Testing Readme_
##### *This readme was written with windows and vscode in mind. Mac and Linux user's mileage may vary!
#
## **Requirements:**
#### Node is required. Type the following in a terminal to check if you have it installed if you are unsure:

```
node --version
```

[Install nodejs](https://nodejs.org/en/download/)
#
#
#### The browser you wish to be tested on needs to be installed on the machine running the tests:
[Install Chrome](https://www.google.com/chrome/)
#
#
#### To install testcafe, in a terminal type

```
npm i testcafe
```
[Testcafe documentation](https://devexpress.github.io/testcafe/documentation/getting-started/)
#
#
### Optional:
#### There is a jenkins plugin for testcafe:
[Plugin and Documentation](https://devexpress.github.io/testcafe/media/team-blog/introducing-the-testcafe-jenkins-plugin.html)
#
#
#### Testcafe studio is an IDE that makes writing tests easy. free 30 day trial. Using this   makes recording tests very easy but if using page models then the code needs to be adjusted in the IDE or after exporting.
[Testcafe Studio](https://www.devexpress.com/products/testcafestudio/#)

[Testcafe Studio documentation](https://docs.devexpress.com/TestCafeStudio/400157/testcafe-studio)
#
#
#### There are VSCode extensions that will make things a little easier:
* [TestCafe Test Runner](https://marketplace.visualstudio.com/items?itemName=romanresh.testcafe-test-runner) - This will let you run tests by right clicking and making a selection
#
#
#
# Writing Page Objects and Tests
* Javascript is used
* See page object model (POM) in [pom folder ](../pom/)
* See tests in [test folder](./tests)
* Don't forget to consult [Testcafe documentation](https://devexpress.github.io/testcafe/documentation/guides/) or [Javascript's documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript) or [Google](https://google.com) when you run into a problem!
  
**POM Code template:**
```js
//import desired items from the testcafe module
import { Selector } from 'testcafe';

//export class so it can be used in tests
export default class name {
  constructor() {
    //list all html elements  
    this.nameOfvariable = Selector("selector")
    this.anotherName = Selector("another Selector")
  }
}
```
example:
```js
import { Selector } from 'testcafe';

export default class LoggedPOM {
  constructor() {
    this.dashboard= Selector("a[title='Dashboard'] > .menu-title")   
  }
}
```
**Test Code template:**
```js
//import any POMs needed for your tests
import class from '../pom/*.tab.js';

//initialize a variable to make it easier on yourself!
const variableName = new className ();

//Every test file needs to have one or more fixtures encapsulated with backticks. 
//A fixture needs to have at least one test but can include as many tests as desired.
  fixture `I am testing this!`

  //the website url to be tested
  .page('url to website')

  //we can also include metadata for our tests. Giving the TFID for instance. We can later run tests just by specifying the meta data!
  .meta('TFID-124', 'TFID-127')

//the actual test. t is for testcontroll and it is a method of testcafe that allows interaction.
test("test name", async t =>{

    //this test expects variableName.variableFromClass to be true
    t.expect(variableName.variableFromClass.exists).ok;
})
```
Test Code example:  
```js
import LoginPOM from '../pom/login.tab.js'
import PlacesPOM from '../pom/places.tab.js'

const Login = new LoginPOM();
const Places = new PlacesPOM();

fixture `Add a new place`
  .page("https://online.staging.traxmate.io/#/pages/places/myPlaces")
  .meta("TFID-39")

test("check for add new tab", async t => {
  .meta("date:4/11/20", "Author:Steve Chapman")
  Login.loginUser(t);
  await t
    .click(Places.places)
    .expect(Places.addNew.exists).ok;
})
```
#
#
#
# Running Tests Locally
#### The following command will run all tests in the tests folder with a headless Chrome
```
npm test

```
#
####
# Running Tests with Jenkins
#### to be implemented


