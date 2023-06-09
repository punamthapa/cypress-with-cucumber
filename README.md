# CYPRESS

Modern days automation testing framework.

# PRE REQUISITES:

-   yarn
-   node: >=12

# INSTALLATION

-   Run `yarn` command.
-   Run `cp .env.example .env` command.
-   Fill the variables in `.env` file.

# Things to Remember:

1. Test must contain assertion rather than just a set of actions. Eg:

**DON'T**

```
it("Adding Email Template", () => {
        cy.get('.ag-flex.col-v-2 > .button').click();

         cy.get('div[name="title"]').click().type(emailTitle)
         cy.get("div[name=subject]").find('p').type(emailSubject)
         cy.get("div[name=content]").find('p').type(emailBody)
         cy.get('.padding-24 > .form > .col-v-5 > .blueButton').click({force:true});
    });
```

**RATHER DO**

```
 it("Should have appropriate tab titles", () => {
        const generalTabTitles = [
            "Product / Partner Type",
            "Discontinued Reasons",
            "Others",
        ];

        cy.get(".nav.nav-tabs.defaultNav> li").each(($el, index) => {
            expect($el).to.have.text(generalTabTitles[index]);
        });
    });
```

2. While writing test spec, splitting test into three sub actions (3 Ps) makes easy. Those 3 Ps are mentioned with proper example below:
    - **Prepare**
        ```
         const generalTabTitles = [
                "Product / Partner Type",
                "Discontinued Reasons",
                "Others",
         ];
        ```
    - **Perform**
        ```
        cy.get(".nav.nav-tabs.defaultNav> li").each
        ```
    - **Predict**
        ```
        expect($el).to.have.text(generalTabTitles[index]);
        ```
3. While writing test code, always make sure to delete the newly added record if there is the action to delete it.

    - For example, if there is feature to `ADD NEW POST`, write test to add new post, assert its existence to verify the test and make sure to delete it at the end and make sure to assert the test to verify that the newly created post is not available in the table or list.

4. In every test make sure to perform following test:
    1. Don't fill any form element. Simply submit the empty form.
    2. Assert the existence of validation error for required form element.
    3. Then check the existence of the validation error.
    4. Fill the required form element.
    5. Submit the form.
    6. If the form lands on same page, make sure the validation errors are cleared.
    7. Better to clear the validation error while we add text to the form field.
5. Each test should be isolated in nature. It means, test spec should be able to run individually. It should not be dependent on any previous test occurrence.

**DON'T**

```
  describe('my form', () => {
     const post = "custom post"

     it('should be able to add new post', () => {
         // logic to add new post

         // logic to assert if post exists in list
     })

     it('should be able to delete newly added post', () => {
        // logic to locate newly added post

        // logic to perform delete action

        // logic to assert of deleted post does not exists in the list.
     })
  })
```

In the above test series, the second test spec depends on the first test specs. This is not a good way to writing test. Rather do it in following manner.

**DO**

```
  describe('my form', () => {
     const post = "custom post"

     it('should be able to add new post and delete', () => {
         // logic to add new post

         // logic to assert if post exists in list

         // locate the recently added post

         // logic to perform delete action

        // logic to assert if deleted post does not exists in the list.
     })
  })
```

# Commands:

Use one of the following command to start runner

-   `yarn cypress:open`

# Directory Structure

| Directory             | Description                                                                                                                                             |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Node Modules          | Used to house dependencies.                                                                                                                             |
| cypress.json          | Enables us to change default settings.                                                                                                                  |
| videos                | Used to store videos of test recordings.                                                                                                                |
| screenshots           | Use to store images of specific tests.                                                                                                                  |
| support               | Used to store custom commands and files. It also includes reusable codes.                                                                               |
| support ->index.js    | First file which cypress investigates; any imports, any libraries, event listener, changes to cypress default behaviour, even the ability to add hooks. |
| support ->commands.js | Used to store command commands, even the ability to override cypress function.                                                                          |
| plugin->index.js      | Extend the cypress functionality; location where we can add plugins.                                                                                    |
| integration           | The main folder where we store our test files. Cypress test runner will look into this folder in order to location test files.                          |
| fixtures              | where we keep our test data objects, mocked objects and any other data which we need for our tests. Mostly we add JSON files.                           |

# Important Links:

-   https://docs.cypress.io/api/cypress-api/cookies#Preserve-Once
#   c y p r e s s - w i t h - c u c u m b e r  
 