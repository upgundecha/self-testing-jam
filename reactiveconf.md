# Cypress.io - the State of the Art End-to-end Testing Tool

Presented at ReactiveConf 2019 in Prague, Czech Republic, [video][video], [slides][slides]

<center>
  <iframe data-cy="talk" width="560" height="315" src="https://www.youtube.com/embed/JL3QKQO80fs"
  frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"
  allowfullscreen></iframe>
</center>

## Main sections

- Lint pyramid [video at 3m46s](https://youtu.be/JL3QKQO80fs?t=226), [slides](https://slides.com/bahmutov/state-of-the-art/#/lint-pyramid) (Prettier, ESLint, `@ts-check`)
- Tests and plugins [video at 7m9s](https://youtu.be/JL3QKQO80fs?t=429), [slides](https://slides.com/bahmutov/state-of-the-art/#/only-tests) (unit, component, web application, visual testing, a11y testing, API testing)
- Code coverage [video at 11m39s](https://youtu.be/JL3QKQO80fs?t=699), [slides](https://slides.com/bahmutov/state-of-the-art/#/code-coverage)
- Splitting end-to-end test via App Actions and checkpoints [video at 20m5s](https://youtu.be/JL3QKQO80fs?t=1205), [slides](https://slides.com/bahmutov/state-of-the-art/#/test-length), read [Split a very long Cypress test into shorter ones using App Actions](https://www.cypress.io/blog/2019/10/29/split-a-very-long-cypress-test-into-shorter-ones-using-app-actions/) blog post

[video]: https://www.youtube.com/watch?v=JL3QKQO80fs
[slides]: https://slides.com/bahmutov/state-of-the-art/

<details>
<summary>Cypress test for the current page</summary>
<!-- fiddle Talk and contents list -->

```js
cy.visit('/reactiveconf.html')
// YouTube player is embedded
cy.contains('Cypress.io - the State of the Art End-to-end Testing Tool')
cy.get('[data-cy=talk]')
  .then($iframe => {
    // this ensures the frame loaded
    cy.wrap($iframe.contents()).should('have.length', 1)
    return cy.wrap($iframe.contents().find("body"))
  })
  .find('.html5-video-player').should('be.visible')
// main sections links
;['Lint pyramid', 'Tests and plugins', 'Code coverage'].forEach(section => {
  cy.contains('li', section).should('be.visible')
})
```

<!-- fiddle-end -->
</details>
