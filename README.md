In this project I have setup cypress with page object model and cucumber BDD framework
For execution report, I have setup cucumber html reports.

1. Installation Process

download nodejs on your machine

Install the below plugins by running commands:

## To install cypress:
npm install cypress --save-dev

## To install cucumber: 
npm install @badeball/cypress-cucumber-preprocessor --save-dev
npm install @bahmutov/cypress-esbuild-preprocessor --save-dev

## To install cypress multiple cucumber html reporter:
npm install multiple-cucumber-html-reporter --save-dev

## reusable commands
Cypress.Commands.add("validateCurrencyApi", () => {
    cy.request({
      method: "GET",
      url: currencyAPI,
      failOnStatusCode: false,
    })
  });

3. Creating cucumber feature file and step defination
@Currency_exchange_API
Feature: Validate currency exchange API
  
  Scenario Outline: Validate currency exchange API
    Given user calls the currency api
    When user should get response status code as <StatusCode>
    Then Count the total number of currencies returned within the response
    Then Verify the currency 'GBP' is shown within the response

    Examples:
      | StatusCode |
      | 200        |
## For example:

Created step defination for this cypress\e2e\step_definitions\api_steps.js
import { Given, When, Then } from "@badeball/cypress-cucumber-preprocessor";

  When("user should get response status code as {int}", (StatusCode) => {
    expect(apiStatusCode).to.equal(StatusCode);
  });

4.	Executing the test in headed and headless mode
## command to run headed mode: 
npx cypress run --headed --spec cypress/e2e/features/*

## command to run headless mode: 
npx cypress run --spec cypress/e2e/features/*

## command to run test with tags: 
npx cypress run --env tags=@ui

## command to run one feature file:
npx cypress run --spec ".\\cypress\\e2e\\features\\API_Test.feature"

## command to generate report: 
node cucumber-html-report.js

5. Steps to execute all the test cases and generate the cucumber html report
   ## step1:
   run this command to install project locally on your machine: npm install --save-dev

   ## step2:
   run this command to execute all the feature files: npx cypress run --spec cypress/e2e/features/*

   ## step3: 
   once all the feature files executed run this command to generate a report: node cucumber-html-report.js

   ## step4: 
   once report is created, it will be available in this folder: \Technical-Test\reports\cucumber-htmlreport.html\index.html
   open index.html to view the detailed execution report